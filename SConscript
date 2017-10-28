import os, sys

Import('env', 'install_perms', 'mypaint_brushes_api_version', 'mypaint_brushes_version')

# Generate a @pkgconfig_name.pc and a @pkgconfig_name-uninstalled.pc
def create_pkgconfig_files(env, pkgconfig_name, api_version, version, description,
                           deps, libs=[], linkflags=[], cflags=[]):

    pkg_info = {
        '@NAME@': pkgconfig_name,
        '@REQUIRES@': ' '.join(deps),
        '@DESCRIPTION@': description,
        '@API_VERSION@': api_version,
        '@VERSION@': version,
        '@LIBS@': ''.join('-l'+lib for lib in libs),
        '@LINKFLAGS@': ' '.join(linkflags),
        '@PREFIX@': env['prefix'],
        '@LIBDIR@': os.path.join(env['prefix'], 'lib'),
        '@DATADIR@': os.path.join(env['prefix'], 'share'),
        '@INCLUDEDIR@': os.path.join(env['prefix'], 'include'),
    }
    pc_file = env.Substfile('%s-%s.pc' % (pkgconfig_name, api_version),
                            "pkgconfig.pc.in", SUBST_DICT=pkg_info)
    install_perms(env, '$prefix/share/pkgconfig', pc_file)

    return pc_file

env = env.Clone()

Export('env')

env.Append(CPPPATH='./')
create_pkgconfig_files(env, 'mypaint-brushes',
                       mypaint_brushes_api_version, mypaint_brushes_version,
                       'MyPaint brushes', deps=[], libs=[], linkflags=[])

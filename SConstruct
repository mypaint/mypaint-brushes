import os, sys
from SCons.Script.SConscript import SConsEnvironment
import SCons.Util

# The API version should stay 1.0 as long as the brushes keep the same
# format, which is also forward-compatible with libmypaint 1.0.
mypaint_brushes_api_version = '1.0'
# This is the actual release version which should be incremented as
# usual to indicate an update.
mypaint_brushes_version = '1.3'

default_prefix = '/usr/local/'

opts = Variables()
opts.Add(PathVariable('prefix', 'autotools-style installation prefix', default_prefix, validator=PathVariable.PathIsDirCreate))

tools = ['default', 'textfile']

env = Environment(ENV=os.environ, options=opts, tools=tools)
opts.Update(env)

# Convenience alias for installing to $prefix
env.Alias('install', '$prefix')

set_dir_postaction = {}
def install_perms(env, target, sources, perms=0644, dirperms=0755):
    """As a normal env.Install, but with Chmod postactions.

    The `target` parameter must be a string which starts with ``$prefix``.
    Unless this is a sandbox install, the permission bits `dirperms` will be
    set on every directory back to ``$prefix``, but not including it. `perms`
    will always be set on each installed file from `sources`.
    """
    assert target.startswith('$prefix')
    install_targs = env.Install(target, sources)
    sandboxed = False
    final_prefix = os.path.normpath(env["prefix"])

    # Set file permissions.
    for targ in install_targs:
        env.AddPostAction(targ, Chmod(targ, perms))
        targ_path = os.path.normpath(targ.get_path())
        if not targ_path.startswith(final_prefix):
            sandboxed = True

    if not sandboxed:
        # Set permissions on superdirs, back to $prefix (but not including it)
        # Not sure if this is necessary with the umask forcing. It might help
        # fix some broken installs.
        for file_targ in install_targs:
            d = os.path.normpath(target)
            d_prev = None
            while d != d_prev and d != '$prefix':
                d_prev = d
                if not set_dir_postaction.has_key(d):
                    env.AddPostAction(file_targ, Chmod(d, dirperms))
                    set_dir_postaction[d] = True
                d = os.path.dirname(d)

    return install_targs

def install_tree(env, dest, path, perms=0644, dirperms=0755):
    assert os.path.isdir(path)
    target_root = os.path.join(dest, os.path.basename(path))
    for dirpath, dirnames, filenames in os.walk(path):
        reltarg = os.path.relpath(dirpath, path)
        target_dir = os.path.join(target_root, reltarg)
        target_dir = os.path.normpath(target_dir)
        filepaths = [os.path.join(dirpath, basename) for basename in filenames]
        install_perms(env, target_dir, filepaths, perms=perms, dirperms=dirperms)

# Common
install_tree(env, '$prefix/share/mypaint-data/{}/'.format(mypaint_brushes_api_version), 'brushes')

Export('env', 'install_tree', 'install_perms', 'mypaint_brushes_api_version', 'mypaint_brushes_version')
brushdata = SConscript('./SConscript')

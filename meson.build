project('com.github.tkashkin.gamehub', 'vala', 'c', version: '0.16.1')

i18n = import('i18n')
gnome = import('gnome')

add_global_arguments('-O0', '-DGETTEXT_PACKAGE="@0@"'.format(meson.project_name()), language: 'c')

if get_option('package') == 'appimage'
	add_global_arguments('-D', 'PKG_APPIMAGE', language: 'vala')
elif get_option('package') == 'flatpak'
	add_global_arguments('-D', 'PKG_FLATPAK', language: 'vala')
endif

if get_option('distro') == 'debian'
	add_global_arguments('-D', 'DISTRO_DEBIAN', '-D', 'PM_APT', language: 'vala')
elif get_option('distro') == 'arch'
	add_global_arguments('-D', 'DISTRO_ARCH', '-D', 'PM_PACMAN', language: 'vala')
endif

if get_option('perf_images_memcache')
	add_global_arguments('-D', 'PERF_IMAGES_MEMCACHE', language: 'vala')
endif

if get_option('perf_gamecard_unload_images')
	add_global_arguments('-D', 'PERF_GAMECARD_UNLOAD_IMAGES', language: 'vala')
endif

conf_data = configuration_data()
conf_data.set('PROJECT_NAME', meson.project_name())
conf_data.set('GETTEXT_PACKAGE', meson.project_name())
conf_data.set('GETTEXT_DIR', join_paths(get_option('prefix'), get_option('localedir')))
conf_data.set('VERSION', meson.project_version())
conf_data.set('GIT_BRANCH', get_option('git_branch'))
conf_data.set('GIT_COMMIT', get_option('git_commit'))
conf_data.set('GIT_COMMIT_SHORT', get_option('git_commit_short'))
conf_data.set('PREFIX', get_option('prefix'))
conf_data.set('DATADIR', join_paths(get_option('prefix'), get_option('datadir')))
conf_data.set('BINDIR', join_paths(get_option('prefix'), get_option('bindir')))
conf_data.set('RUNTIME', get_option('runtime'))

subdir('data')
subdir('src')
subdir('po')

meson.add_install_script('meson/post_install.py')

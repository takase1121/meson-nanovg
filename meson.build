project('nanovg', ['c'], 
         version       : '0.1.0',  
         license       : ['ZLIB'],
         meson_version : '>= 0.49.0')




name = 'nanovg'




system     = build_machine.system()
cpu        = build_machine.cpu()
cpu_family = build_machine.cpu_family()

cc    = meson.get_compiler('c')
cc_id = cc.get_id() 

build_examples = get_option('build_examples')

includes  = []
sources   = []
c_args    = []
link_args = []




if system not in ['windows']
    error('Script (meson.build) not prepared for your platform yet.')
endif

if system == 'windows' and cc_id not in ['msvc']
    error('Script (meson.build) not prepared for your compiler yet.')
endif




include = include_directories('src')

sources = ['src/fontstash.h',
           'src/nanovg.c',
           'src/nanovg.h',
           'src/nanovg_gl.h',
           'src/nanovg_gl_utils.h',
           'src/stb_image.h',
           'src/stb_truetype.h']

c_args    = ['-D_CRT_SECURE_NO_WARNINGS']



  
static_lib_name        = name
static_lib_name_prefix = []
static_lib_name_suffix = []

if system == 'windows' and cc_id == 'msvc'  
    static_lib_name       += '_static'
    static_lib_name_prefix = ''
    static_lib_name_suffix = 'lib'
endif

nanovg_static = static_library(static_lib_name,
                             name_prefix         : static_lib_name_prefix, 
                             name_suffix         : static_lib_name_suffix,
                             include_directories : include,
                             sources             : sources,
                             c_args              : c_args, 
                             link_args           : link_args,
                             install             : true)

nanovg_static_dep = declare_dependency(include_directories : include,
                                       link_with           : nanovg_static)

nanovg_dep = nanovg_static_dep




if get_option('build_examples')
  if not meson.is_subproject()
    subdir('example')
  else
    warning('The option ' + name + ':' + 'build_examples' + ' not work in subproject.')
  endif 
endif




install_headers('src/nanovg.h', 
                'src/nanovg_gl.h', 
                'src/nanovg_gl_utils.h',
                 subdir : 'NANOVG')

install_data(['LICENSE.txt'],
               rename : ['LICENSE.ZLIB'],
               install_dir : 'share/licenses/nanovg')

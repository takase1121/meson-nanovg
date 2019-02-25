
glew_project = subproject('glew')
glew_dep     = glew_project.get_variable('glew_dep')

glfw_project = subproject('glfw')
glfw_dep     = glfw_project.get_variable('glfw_dep')

opengl_registry_project = subproject('opengl-registry')
opengl_registry_dep = opengl_registry_project.get_variable('opengl_registry_dep')

opengl_dep = cc.find_library('opengl32', required: true)
glu_dep    = cc.find_library('glu32', required: true)

c_args += ['-DNANOVG_GLEW']

include = include_directories('.')

executable('example_gl2' 
		   ,include_directories : [include]
           ,sources             : ['example_gl2.c', 'demo.c', 'perf.c']
           ,c_args              : c_args
           ,dependencies        : [nanovg_dep, glfw_dep, glew_dep, opengl_dep, opengl_registry_dep]
           ,install             : true)




install_data(['entypo.ttf',
			  'images.txt',
			  'LICENSE_OFL.txt',
			  'NotoEmoji-Regular.ttf',
			  'Roboto-Bold.ttf',
			  'Roboto-Light.ttf',
			  'Roboto-Regular.ttf',
			  'screenshot-01.png',
			  'screenshot-02.png'],
               install_dir : 'example')

install_subdir('images', install_dir : 'example')
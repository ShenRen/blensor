# ***** BEGIN GPL LICENSE BLOCK *****
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either version 2
# of the License, or (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software Foundation,
# Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301, USA.
#
# The Original Code is Copyright (C) 2006, Blender Foundation
# All rights reserved.
#
# The Original Code is: all of this file.
#
# Contributor(s): Jacques Beaurain.
#
# ***** END GPL LICENSE BLOCK *****

set(INC
	.
	../blenkernel
	../blenlib
	../bmesh
	../imbuf
	../makesdna
	../makesrna

	# For node muting stuff...
	../nodes
	../nodes/intern

	../../../intern/glew-mx
	../../../intern/guardedalloc
	../../../intern/smoke/extern
)

set(INC_SYS
	${GLEW_INCLUDE_PATH}
)

set(SRC
	intern/gpu_buffers.c
	intern/gpu_codegen.c
	intern/gpu_draw.c
	intern/gpu_extensions.c
	intern/gpu_init_exit.c
	intern/gpu_material.c
	intern/gpu_simple_shader.c
	intern/gpu_select.c
	intern/gpu_compositing.c
	intern/gpu_debug.c

	shaders/gpu_shader_fx_lib.glsl
	shaders/gpu_shader_fx_ssao_frag.glsl
	shaders/gpu_shader_fx_dof_frag.glsl
	shaders/gpu_shader_fx_dof_vert.glsl
	shaders/gpu_shader_fx_dof_hq_frag.glsl
	shaders/gpu_shader_fx_dof_hq_vert.glsl
	shaders/gpu_shader_fx_dof_hq_geo.glsl
	shaders/gpu_shader_fx_vert.glsl
	shaders/gpu_shader_material.glsl
	shaders/gpu_shader_sep_gaussian_blur_frag.glsl
	shaders/gpu_shader_sep_gaussian_blur_vert.glsl
	shaders/gpu_shader_simple_frag.glsl
	shaders/gpu_shader_simple_vert.glsl
	shaders/gpu_shader_vertex.glsl
	shaders/gpu_shader_vsm_store_frag.glsl
	shaders/gpu_shader_vsm_store_vert.glsl
	shaders/gpu_shader_fx_depth_resolve.glsl

	GPU_buffers.h
	GPU_draw.h
	GPU_debug.h
	GPU_extensions.h
	GPU_glew.h
	GPU_init_exit.h
	GPU_material.h
	GPU_simple_shader.h
	GPU_select.h
	GPU_compositing.h
	intern/gpu_codegen.h
	intern/gpu_private.h
)

data_to_c_simple(shaders/gpu_shader_material.glsl SRC)
data_to_c_simple(shaders/gpu_shader_sep_gaussian_blur_frag.glsl SRC)
data_to_c_simple(shaders/gpu_shader_sep_gaussian_blur_vert.glsl SRC)
data_to_c_simple(shaders/gpu_shader_simple_frag.glsl SRC)
data_to_c_simple(shaders/gpu_shader_simple_vert.glsl SRC)
data_to_c_simple(shaders/gpu_shader_vertex.glsl SRC)
data_to_c_simple(shaders/gpu_shader_vertex_world.glsl SRC)
data_to_c_simple(shaders/gpu_shader_vsm_store_frag.glsl SRC)
data_to_c_simple(shaders/gpu_shader_vsm_store_vert.glsl SRC)
data_to_c_simple(shaders/gpu_shader_fx_vert.glsl SRC)
data_to_c_simple(shaders/gpu_shader_fx_ssao_frag.glsl SRC)
data_to_c_simple(shaders/gpu_shader_fx_dof_frag.glsl SRC)
data_to_c_simple(shaders/gpu_shader_fx_dof_vert.glsl SRC)
data_to_c_simple(shaders/gpu_shader_fx_dof_hq_frag.glsl SRC)
data_to_c_simple(shaders/gpu_shader_fx_dof_hq_vert.glsl SRC)
data_to_c_simple(shaders/gpu_shader_fx_dof_hq_geo.glsl SRC)
data_to_c_simple(shaders/gpu_shader_fx_depth_resolve.glsl SRC)
data_to_c_simple(shaders/gpu_shader_fx_lib.glsl SRC)

if(WITH_GAMEENGINE)
	add_definitions(-DWITH_GAMEENGINE)
endif()

if(WITH_MOD_SMOKE)
	add_definitions(-DWITH_SMOKE)
endif()

add_definitions(${GL_DEFINITIONS})

if(WITH_IMAGE_DDS)
	add_definitions(-DWITH_DDS)
endif()


blender_add_lib(bf_gpu "${SRC}" "${INC}" "${INC_SYS}")


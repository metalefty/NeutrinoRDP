# FreeRDP: A Remote Desktop Protocol Client
# FreeRDP cmake build script
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

set(XRDPVR_SRCS
	xrdpvr_audio.c
	xrdpvr_main.c
	xrdpvr_player.c)

include_directories(../drdynvc)

add_library(xrdpvr ${XRDPVR_SRCS})
set_target_properties(xrdpvr PROPERTIES PREFIX "")

target_link_libraries(xrdpvr freerdp-utils ${FFMPEG_LIBRARIES} -lavformat)

install(TARGETS xrdpvr DESTINATION ${FREERDP_PLUGIN_PATH})

if(WITH_ALSA)
	add_subdirectory(alsa)
endif()


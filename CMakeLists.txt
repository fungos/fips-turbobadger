#
# project: fips-turbobadger
#

if (NOT FIPS_IMPORT)
    cmake_minimum_required(VERSION 2.8)
    get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
    include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    fips_setup()
    fips_project(fips-turbobadger)
endif()

option(TB_ENABLE_RTTI "Do not disable RTTI" OFF)

if (NOT FIPS_EXCEPTIONS)
    set(TB_NO_EXCEPTIONS "-fno-exceptions")
endif()

if (NOT TB_ENABLE_RTTI)
    set(TB_NO_RTTI "-fno-rtti")
endif()

if (FIPS_WINDOWS)
    add_definitions(-DGLFW_EXPOSE_NATIVE_WIN32)
    add_definitions(-DGLFW_EXPOSE_NATIVE_WGL)
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
    add_definitions(-D_CRT_NONSTDC_NO_DEPRECATE)
    add_definitions(-DTB_USE_CURRENT_DIRECTORY)
elseif (FIPS_LINUX)
elseif (FIPS_MACOS)
    add_definitions(-DMACOSX)
    add_definitions(-Dnullptr=0)
    add_definitions(-DTB_USE_CURRENT_DIRECTORY)
endif()

fips_begin_lib(turbobadger)
    include_directories(turbobadger/src/tb)

    fips_dir(turbobadger/src/tb/animation)
    fips_files(
        tb_animation_utils.h
        tb_animation.cpp
        tb_widget_animation.h
        tb_animation.h
        tb_widget_animation.cpp
    )
    fips_dir(turbobadger/src/tb/utf8)
    fips_files(
        utf8.cpp
        utf8.h
    )
    fips_dir(turbobadger/src/tb/renderers)
    fips_files(
        tb_renderer_gl.cpp
        tb_renderer_batcher.cpp
        tb_renderer_gl.h
        tb_renderer_batcher.h
    )
    fips_dir(turbobadger/src/tb/thirdparty)
    fips_files(
        stb_image.h
        stb_truetype.h
    )
    fips_dir(turbobadger/src/tb/parser)
    fips_files(
        tb_parser.h
        tb_parser.cpp
    )
    fips_dir(turbobadger/src/tb/image)
    fips_files(
        tb_image_manager.cpp
        tb_image_widget.cpp
        tb_image_widget.h
        tb_image_manager.h
    )
    fips_dir(turbobadger/src/tb)
    fips_files(
        tb_addon.cpp
        tb_bitmap_fragment.cpp
        tb_clipboard_dummy.cpp
        tb_clipboard_glfw.cpp
        tb_clipboard_win.cpp
        tb_color.cpp
        tb_core.cpp
        tb_debug.cpp
        tb_dimension.cpp
        tb_editfield.cpp
        tb_file_posix.cpp
        tb_font_renderer.cpp
        tb_font_renderer_freetype.cpp
        tb_font_renderer_stb.cpp
        tb_font_renderer_tbbf.cpp
        tb_geometry.cpp
        tb_hash.cpp
        tb_hashtable.cpp
        tb_id.cpp
        tb_image_loader_stb.cpp
        tb_inline_select.cpp
        tb_language.cpp
        tb_layout.cpp
        tb_linklist.cpp
        tb_list.cpp
        tb_menu_window.cpp
        tb_message_window.cpp
        tb_msg.cpp
        tb_node_ref_tree.cpp
        tb_node_tree.cpp
        tb_object.cpp
        tb_popup_window.cpp
        tb_renderer.cpp
        tb_scroll_container.cpp
        tb_scroller.cpp
        tb_select.cpp
        tb_select_item.cpp
        tb_skin.cpp
        tb_skin_util.cpp
        tb_str.cpp
        tb_style_edit.cpp
        tb_style_edit_content.cpp
        tb_system_android.cpp
        tb_system_linux.cpp
        tb_system_win.cpp
        tb_tab_container.cpp
        tb_tempbuffer.cpp
        tb_toggle_container.cpp
        tb_value.cpp
        tb_widget_skin_condition_context.cpp
        tb_widget_value.cpp
        tb_widgets.cpp
        tb_widgets_common.cpp
        tb_widgets_listener.cpp
        tb_widgets_reader.cpp
        tb_window.cpp
        tb_addon.h
        tb_bitmap_fragment.h
        tb_color.h
        tb_config.h
        tb_core.h
        tb_debug.h
        tb_dimension.h
        tb_editfield.h
        tb_font_desc.h
        tb_font_renderer.h
        tb_geometry.h
        tb_hash.h
        tb_hashtable.h
        tb_id.h
        tb_inline_select.h
        tb_language.h
        tb_layout.h
        tb_linklist.h
        tb_list.h
        tb_menu_window.h
        tb_message_window.h
        tb_msg.h
        tb_node_ref_tree.h
        tb_node_tree.h
        tb_object.h
        tb_popup_window.h
        tb_renderer.h
        tb_scroll_container.h
        tb_scroller.h
        tb_select.h
        tb_select_item.h
        tb_skin.h
        tb_skin_util.h
        tb_sort.h
        tb_str.h
        tb_style_edit.h
        tb_style_edit_content.h
        tb_system.h
        tb_tab_container.h
        tb_tempbuffer.h
        tb_toggle_container.h
        tb_types.h
        tb_value.h
        tb_widget_skin_condition_context.h
        tb_widget_value.h
        tb_widgets.h
        tb_widgets_common.h
        tb_widgets_listener.h
        tb_widgets_reader.h
        tb_window.h
    )
    fips_dir(turbobadger/src/tb/tests)
    fips_files(
        tb_test.cpp
        tb_test.h
        test_tb_color.cpp
        test_tb_dimension.cpp
        test_tb_geometry.cpp
        test_tb_linklist.cpp
        test_tb_node_ref_tree.cpp
        test_tb_object.cpp
        test_tb_parser.cpp
        test_tb_space_allocator.cpp
        test_tb_style_edit.cpp
        test_tb_tempbuffer.cpp
        test_tb_test.cpp
        test_tb_value.cpp
        test_tb_widget_value.cpp
    )
fips_end_lib()


if (NOT FIPS_IMPORT)
    if (FIPS_MACOS OR FIPS_LINUX OR FIPS_WINDOWS)
        fips_begin_app(demo windowed)
            include_directories(turbobadger/Demo)
            include_directories(turbobadger/Demo/demo01)
            include_directories(turbobadger/Demo/platform)
            fips_dir(turbobadger/Demo/platform)
            fips_files(
                Application.cpp
                Application.h
                glfw_extra.h
                glfw_extra_linux.cpp
                glfw_extra_win.cpp
                port_glfw.cpp
            )
            fips_dir(turbobadger/Demo/demo01)
            fips_files(
                Demo.h
                Demo01.cpp
                ListWindow.cpp
                ListWindow.h
                ResourceEditWindow.cpp
                ResourceEditWindow.h
            )
            fips_deps(turbobadger glfw3)

            if (FIPS_WINDOWS)
                fips_libs(opengl32 winmm)
            endif()

            if (FIPS_LINUX)
                fips_libs(X11 Xrandr Xi Xinerama Xxf86vm Xcursor GL m)
            endif()

            if (FIPS_MACOS)
                fips_libs(m)
            endif()
        fips_end_app()
    endif()
    if (FIPS_ANDROID)
        # demo android
    endif()

    if (FIPS_CLANG)
        set_target_properties(demo PROPERTIES COMPILE_FLAGS "${TB_NO_EXCEPTIONS} ${TB_NO_RTTI} -Wall -Wextra -Wno-unused-parameter -Wno-unused-function")
    elseif(FIPS_GCC)
        set_target_properties(demo PROPERTIES COMPILE_FLAGS "${TB_NO_EXCEPTIONS} ${TB_NO_RTTI} -Wall -Wextra -Wno-unused-parameter -Wno-unused-function")
    endif()
endif()


if (FIPS_CLANG)
    set_target_properties(turbobadger PROPERTIES COMPILE_FLAGS "${TB_NO_EXCEPTIONS} ${TB_NO_RTTI} -Wall -Wextra -Wno-unused-parameter -Wno-unused-function")
elseif(FIPS_GCC)
    set_target_properties(turbobadger PROPERTIES COMPILE_FLAGS "${TB_NO_EXCEPTIONS} ${TB_NO_RTTI} -Wall -Wextra -Wno-unused-parameter -Wno-unused-function")
elseif(FIPS_MSVC)
    if (NOT FIPS_EXCEPTIONS)
        string(REPLACE "/EHsc" "" CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS}) # -fno-exceptions
    endif()

    if (NOT TB_ENABLE_RTTI)
        string(REPLACE "/GR" "" CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS}) # -fno-rtti
    endif()

    string(REPLACE "/WX" "/WX-" CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS}) # disable warning as error due GCC pragmas
endif()

if (NOT FIPS_IMPORT)
    fips_finish()
endif()


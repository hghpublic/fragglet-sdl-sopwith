
target_sources(${target} PRIVATE
        font.h
        pcsound.h
        std.h
        swasynio.c   swasynio.h
        swauto.c     swauto.h
        swcollsn.c   swcollsn.h
        swconf.c     swconf.h
        swend.c      swend.h
        swgames.c    swgames.h
        swgrpha.c    swgrpha.h
        sw.h
        swinit.c     swinit.h
        swmain.c     swmain.h
        swmenu.c     swmenu.h
        swmove.c     swmove.h
        swobject.c   swobject.h
        swsound.c    swsound.h
        swsplat.c    swsplat.h
        swstbar.c    swstbar.h
        swsymbol.c   swsymbol.h
        swtext.c     swtext.h
        swtitle.c    swtitle.h
        hiscore.c    hiscore.h
        tcpcomm.c    tcpcomm.h
        timer.h
        touch_area.c
        video.c      video.h
        yocton.c     yocton.h
)

target_include_directories(${target} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
add_subdirectory(sdl)

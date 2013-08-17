---
layout: sdl_lesson
title: "Lesson 0: Linux Command Line"
description: "Setting Up SDL"
category: "SDL2 Tutorials"
tags: ["SDL2", "Linux"]
---
{% include JB/setup %}

To build the projects on Linux we'll be using a simple makefile that will setup the include and library
dependencies for us. The makefile assumes that your SDL libraries are installed under `/usr/local/lib`
and the headers are under `/usr/local/include`. These are the install locations if you built the
project through cmake. If you've installed it through your package manager or placed the libraries
and headers elsewhere you may need to change these paths to match your installation.

If you're unfamiliar with Makefiles a basic introduction can be found [here](http://mrbook.org/tutorials/make/)

The Makefile
-
{% highlight makefile %}
CXX = g++
# Update these paths to match your installation
SDLLIB = -L/usr/local/lib -lSDL2
SDLINCLUDE = -I/usr/local/include
# You may need to change -std=c++11 to -std=c++0x if your compiler is a bit older
CFLAGS = -Wall -c -std=c++11 $(SDLINCLUDE)
LDFLAGS = $(SDLLIB)
EXE = SDL_Lesson0

all: $(EXE)

$(EXE): main.o
	$(CXX) $(LDFLAGS) $< -o $@

main.o: main.cpp
	$(CXX) $(CFLAGS) $< -o $@

clean:
	rm *.o && rm $(EXE)
{% endhighlight %}
<br />

The Test Program
-
To make sure everything has installed properly we’ll try compiling and running a very simple program that
initializes the various SDL systems and then quits. If anything goes wrong, an error message will be
printed out. The source file should be titled `main.cpp`, or you can change the main.o build dependency
in the makefile to match your source file.

If you installed SDL through cmake you may need to copy `libSDL2-2.0.so.0` from the install directory
`/usr/local/lib` into `/usr/lib` so that it can be found at run time. Alternatively you can add 
`/usr/local/lib` to your library path or if it's already in your path you can skip this step entirely.

{% highlight c++ %}
#include <iostream>
#include <SDL2/SDL.h>

int main(int argc, char **argv){
	if (SDL_Init(SDL_INIT_EVERYTHING) != 0){
		std::cout << "SDL_Init Error: " << SDL_GetError() << std::endl;
		return 1;
	}
	SDL_Quit();

	return 0;
}
{% endhighlight %}
<br />

The program should run successfully but nothing should appear to happen if you've configured everything
properly. If an error occurs make sure you've followed all the setup steps properly.

End of Lesson 0
-
If you're having any trouble setting up SDL please leave a comment below.

I'll see you again soon in Lesson 1: Hello World! (Coming soon!). The old version is accessible 
[here](http://twinklebeardev.blogspot.com/2012/07/lesson-1-hello-world.html).
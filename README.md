# ST7565_Menu
An example Arduino menu and user interface based on the API generated by Alexander Hiam

Extensions from the previous menu implementations:
  1. alters the menu screens slightly, and only updates the screen if a button has been pressed. This dramatically 
    decreases the runtime of the void loop, allowing this code to be compatible with arduino functionalities requiring high frequency
	operations, such as data aquisition or high frequency pin mode changes.
  2. Alters the menu screen layouts slightly to provide a more streamlined interface 
  3. provides the code structure to easily incorporate bitmaps designs into the display, based off of complex images  


The original API can be found at https://github.com/alexanderhiam/ST7565_Menu


************************************************************************
ST7565 Menu - Michael Rees
Created: 5/2015
Author: Michael Rees - michael.rees@duke.edu

 Copyright (c) 2015,2016 - Michael Rees

 This program is free software: you can redistribute it and/or modify
 it under the terms of the GNU General Public License as published by
 the Free Software Foundation, either version 3 of the License, or
 (at your option) any later version.

 This program is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the 
 GNU General Public License for more details.

 You should have received a copy of the GNU General Public License
 along with this program.  If not, see <http://www.gnu.org/licenses/>.
************************************************************************

This library uses Adafruit's ST7565 to provide a simple API for creating 
a menu based user interface. See example sketches and API description
below for more details.

Included is a version of the Adafruit ST7565 library modified to include
an #ifndef wrapper in the ST7565.h file. This library won't work without
the modification. 

To install library place the whole ST7565_Menu/ folder in your Arduino 
libraries directory, then drag the ST7565/ folder up into the libraries
directory as well, replacing your current Adafruit library if it exists.


ST7565_Menu should contain:
 -ST7565_Menu.cpp
 -ST7565_Menu.h
 -keywords.txt
 -README
 -COPYING
 -ST756/

API:
 -Menu(uint8_t up_pin, uint8_t down_pin, uint8_t select_pin, ST7565 *lcd)
   Creates and returns an instance of the Menu object. up_, down_ and 
   select_pins are the IO pins where the control buttons are connected.
   The buttons must be configured active-low with external pullups.
   lcd should be the address of an instance of the Adafruit ST7565 object
   (e.g. &ST7565_instance).

 -Menu.set_title(char *title)
   Sets the title string that is displayed on the first line of the LCD.
   The title will remain on the first line during scrolling of the menu.
   Will be blank if not set.

 -Menu.add_item(char *label)
   Adds a functionless item to the menu.

 -Menu.add_item(char *label, void (*function)(void))
   Adds an item to the menu. When selected the given function will be 
   called.

 -Menu.add_item(char *label, int value, void (*function)(int))
   Adds an item to the menu. When selected the given function will be 
   passed the given integer value.

 -Menu.add_draw_function(void (*function)(void))
   Adds a function that will be just before the menu is drawn. This is
   where other graphics should be drawn to the LCD. Menu can only have
   one draw function.

 -Menu.add_timeout_function(int timeout, void (*function)(void))
   Adds a function that will be called after Menu.update() has been 
   called the given number of times without any of the menu controls 
   being pressed. In order to have other controls or events restart the
   timeout count, one should set Menu.timeout_counter to 0.

 -Menu.draw()
   Redraws the whole menu; does not update read controls or increment 
   timeout counter. Shouldn't normally need to be called.

 -Menu.update()
   This function should be called each time through the main loop to
   use the menu.  

 -Menu.clear()
   Completely resets the menu. This should be called before creating 
   new menus.

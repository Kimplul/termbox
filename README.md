# Termbox with true color support

This is a fork of [termbox](https://github.com/nsf/termbox) that adds true color
support.

Main changes in the api include:
+ Addition of ```TB_OUTPUT_TRUECOLOR``` macro
+ Addition of ```tb_truecolor``` struct, with ```uint8_t``` member variables ```r```, ```g```, ```b```.
+ ```tb_set_clear_attributes``` now takes two ```tb_truecolor``` structs in
addition to what is stated in the original repo. Foreground and background.
+ ```tb_change_cell``` similarly takes two ```tb_truecolor```structs.

# Example:

```
#include <iostream>
#include <termbox.h>

int main(){
    tb_event ev;

    tb_select_output_mode(TB_OUTPUT_TRUECOLOR);
    tb_init();

    for(uint8_t x = 0; x < 20; x++){
        for(uint8_t y = 0; y < 10; y++){
            tb_truecolor fg, bg;
            fg.r = 12*x; bg.r = 12*x;
            fg.g = 25*y; bg.g = 25*y;
            fg.b =    0; bg.b =    0;

            tb_change_cell(x, y, L'\u2583', 0, 0, fg, bg);
        }
    }

    tb_present();
    tb_poll_event(&ev);
    tb_shutdown();
    return 0;
}
```

Compile with ```-ltermbox```.

Valentin Franco 4°1° Avionica
Ayudante:Britez Luis


#include <stdio.h>
#include "pico/stdlib.h"

/* Estructura para el LCD */
typedef struct {
  uint8_t rs;		/* GPIO de RS */
  uint8_t en;		/* GPIO de EN */
  uint8_t d4;		/* GPIO de D4 */
  uint8_t d5;		/* GPIO de D5 */
  uint8_t d6;		/* GPIO de D6 */
  uint8_t d7;		/* GPIO de D7 */
} lcd_t;

/* Inline functions */

/* Genera una estructura por defecto para el LCD */
static inline lcd_t lcd_get_default_config(void) {
  lcd_t lcd = { 0, 1, 2, 3, 4, 5 };
  return lcd;
}

/* Obtiene la mascara de pines de datos */
static inline uint32_t lcd_get_data_mask(lcd_t lcd) {
  return 1 << lcd.d4 | 1 << lcd.d5 | 1 << lcd.d6 | 1 << lcd.d7;
}

/* Obtiene la mascara de pines conectadas al LCD */
static inline uint32_t lcd_get_mask(lcd_t lcd) {
  return 1 << lcd.rs | 1 << lcd.en | lcd_get_data_mask(lcd);
}

/* Function prototypes */
void lcd_init(lcd_t lcd);
void lcd_put_nibble(lcd_t lcd, uint8_t nibble);
void lcd_put_command(lcd_t lcd, uint8_t cmd);
void lcd_putc(lcd_t lcd, char c);
void lcd_puts(lcd_t lcd, const char* str);
void lcd_clear(lcd_t lcd);
void lcd_go_to_xy(lcd_t lcd, uint8_t x,  uint8_t y);

/* Programa principal */

int main() {
	/* Inicializo el USB */
  stdio_init_all();
	/* Obtengo una variable para elegir los pines del LCD */
  lcd_t lcd = lcd_get_default_config();
	/* Por defecto, los pines son:
	 	- GP0 (RS)
		- GP1 (EN) 
		- GP2 (D4)
		- GP3 (D5)
		- GP4 (D6)
		- GP5 (D7)
		
		Si quieren cambiar alguno pueden hacerlo como lcd.d5 = 6 por ejemplo */
  
	/* Inicializo el LCD */
	lcd_init(lcd);
	char txt[]="hola como estas amigo franvi!";
	;char aux[16];
  ;while (true) {
	for(int j=0; j< 16;j++){
		lcd_clear(lcd);
		for(int i=0;i<16;i++){
		aux[i]=txt[i+j];
		}
		lcd_puts(lcd,aux);
    /* Espero medio segundo */
		sleep_ms(250);
  	}			
		}
		

	
}

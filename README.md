# Tutorial del curso de Diseño Lógico evidencias: 

## Primera parte: Instalacion de Herramientas

Primero se procede a instalar los programas necesarios en este caso, VScode, sus extensiones, OSS-Cad_Suite, y GNU-Make

img 1, 2 

## Segunda parte: Uso del toolchain para diseño en FPGA

Se clona el repositorio para tener un editable propio (como ya se puede apreciar). Se inicializa tambien la terminal del toolchain como se aprecia en la imagen mostrada anteriormente. Seguidamente se testea que este bien instalado con el comando yosys.

img 3

Seguidamente se dirije por medio de cd .direccion al build del ejemplo 1 donde se corre make test y make wv para apreciar el siguiente grafico:

img 4

se utiliza make synth para verificar sintaxis y sintetisar disenos, make pnr para generar un archivo .json como se aprecia en la siguiente imagen.

img 5

se corre el comando make bitstream que crea un archivo .fs con la info del diseno.

img 6

Finalmente se usan los comandos make load y make all para cargar y ejecutar la informacion en la fpga. Para el caso de blinky LED, olvide tomar fotografia pero se encendian las luces integradas del FPGA en cierto patron. En el caso de segundo ejemplo lcd spi se realiza el mismo proceso y por su redundancia lo omitire pero el resultado fue una bandera de Costa Rica en el display del FPGA que se veia como la imagen siguiente.

img 7

## Tercera parte: Descarga de la plantilla. 

Esta parte me parece que tambien se puede obviar puesto a que para armar este repositorio se hizo el mismo proceso.

## Cuarta parte: Primer diseño... Display 7 segmentos

Para esta parte se deben hacer un par de aclaraciones. Es importante indicar que en la bodega; a diferencia de lo solicitado en la lista de componentes referente a la compuerta AND especificada (de 4 compuertas con 2 entradas cada una) nos entregaron una con 2 compuertas de 4 entradas cada una. Segun mis calculos del mapa de Karnaugh, requeria mas de dos operaciones de AND por lo que intente sustituirlo por el segmento A que necesitaba menos de estos.

Se hizo la instalacion del circuito en la protoboard siguiendo los siguientes pasos:
Identificando los pines de 5V y GND de la FPGA
Conectarlos a los pines 7 (GND) y 14 (V_cc/5V) de todas las compuertas para que funcionen
Conectar tambien los 5V a las patillas del switch y en mi caso a ambas patillas centrales del display
Calcular la ecuacion simplificada (modificada para el segmento A) que queda B+C+A'D
Realizar las operaciones primero sacando A' con el not, despues sacar A'D con el and, y finalmente con el or sacar primero B+C y despues (B+C)+(A'D), sacar el resultado a una resistencia de unos 300 ohm y posteriormente pasarlo a la patilla A del display de 7 segmentos para que quede de la siguiente manera:

img8

Asimismo, con la parte del codigo del ejemplo 3, se pide que se haya la modificacion que el test no imprima nada si es correcto y se logra eliminando la parte comentada

img 9

Adicionalmente se editan los segmentos como dicen las indicaciones:

img 10

Tras correr de la misma manera los primeros comandos en orden igual al presentado anteriormente, presenta un error en make bitstream que tras revisar cuestiones sugeridas en el documento como los pines no logre arreglar. Como prueba se demuestra que al generar el make wv hay algo inusual que genera que una parte de este este en rojo.

img 11



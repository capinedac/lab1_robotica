# Laboratorio 1 - Robótica Industrial No.1 
Equipo de trabajo: 
- Luis Alberto Chavez Castro
- Camilo Pineda Correa
 
## Desarrollo de la herramienta
Para el proceso de fabricación de la herramienta, este se desarrolló primero físicamente, teniendo en cuenta las medidas de ajuste con el portaherramienta para su implementación, y a partir de este se generó el modelo CAD con ayuda del software Catia.
 
La herramienta tuvo una primera versión que fue probada, se puede visualizar en su montaje al robot articulado:
 
![Herramienta v1](/imagenes/herramientav1.jpeg)
 
Su versión final diseñada es la siguiente:
 
![Foto herramienta](/imagenes/herramienta.jpg)
![Foto 2 herramienta](/imagenes/herramienta2.jpg)
 
Y su modelo CAD obtenido fue:
 
![CAD herramienta](/imagenes/herramientaCAD.bmp)
 
Se construyó una herramienta inicial la cual se buscó desde un comienzo que su eje primitivo de diseño no se encontrara sobre el eje Z del TCP del plato portaherramientas a fin de evitar las singularidades del robot, para esto las dos primitivas de diseño empleadas fueron dos líneas coplanares que no fueran paralelas con un ángulo entre ellas de 120º.
Además al realizar las primeras pruebas con el manipulador, se encontró que la herramienta vibraba mucho y era inestable a la hora de ser colocada sobre la superficie plana para trazar, por lo que se planteó un incremento en los  momentos de inercia que evitase el movimiento de la pieza, sin embargo como uno de los requerimientos de diseño que presentados considera el bajo peso para la reducción de cargas inerciales del robot, se planteó emplear materiales pero todos en diferentes medidas incrementaron los momentos de inercia, así que se planteó realizar una ampliación de la geometría de la zona que presentaba la mayor oscilación con materiales ligeros, de fácil consecución y simétricos, para lo cual el candidato seleccionado resultó ser un envase PET (polietilen-Tereftalato) de agua de 500ml, el cual por su peso ligero y alta resistencia mecánica al desgaste por vibraciones, entregó un gran comportamiento al mantener el bajo peso y reducir considerablemente la vibración de la herramienta.

Además de la reducción de cargas inercial , el candidato PET también aportó dos funcionalidades inesperadas, la primera al tener tapa enroscable se puede crear una pieza de ensamble y desensamble cómodo sobre el manipulador que además permite la orientación de la herramienta, sin interferir con la fijación del portaherramientas ni del plato porta herramienta del manipulador IRB140. La segunda cualidad hallada es la posibilidad de aportar carga inercial al emplear el envase como un receptáculo capaz de albergar un volumen de 7 onzas aproximadamente, suficiente para emplear la herramienta de geometría definida en entornos con diversas cargas inerciales que puedan ayudar a realizar experimentos de caracterización inercial de componentes. 
 
![plano herramienta](/imagenes/herramientaPlano.jpg)
 
En el diseño se cuenta con un sistema de suspensión telescópico entre el marcador y la estructura de forma que hay 40mm entre la punta del marcador y la posición de máxima retracción del elemento a fin de buscar evitar cargas sobre el manipulador robótico; está diseñado de forma predictiva ante una posible colisión, que inicialmente causaría la retracción del elemento antes de activar una pieza fusible causando la fractura de la tapa del envase con lo que la pieza se desprende del manipulador evitando posibles daños al mismo.
 
El sistema de suspensión telescópico se compone de un par de tubos coaxiales
con un ajuste deslizante, lubricado por aceite SAE50, al interior del tubo de mayor diámetro (22mm exterior) también se aloja un resorte, con k=0.1N/m.
 
 
 
## Desarrollo del plano de trabajo y letras
Para el plano de trabajo, este es un tablero inclinado de dimensiones 300mm x 300mm y una inclinación de 45°, diseñado con el software Inventor. Sobre el plano que se trabaja se escribió el texto con las letras a escribir, permitiendo realizar un grabado a través de extrusión de corte de esa figura, lo que permitía contar con el perfil a seguir a través del contorno generado:
 
![CAD plano45](/imagenes/plano45.jpg)
 
 
 
## Trabajo en RobotStudio.  
Inicialmente se genera la estación de trabajo con el robot articulado IRB 140 y su respectivo controlador RobotWare 6.13.04. Luego se procede a importar la geometría de la herramienta y ajustarla al portaherramientas:
 
![Importar herramienta RobotStudio](/imagenes/robotStudio1.jpg)  
 
Fue necesario hacer una modificación en cuanto a orientación y desplazamiento para un mejor ajuste, por lo que se accede a la siguiente configuración:
 
![Ajustar herramienta RobotStudio](/imagenes/robotStudio2.jpg)  
 
Luego, se continúa generando el TCP de la herramienta, para ello se crea el dato de la herramienta teniendo en cuenta la geometría de la herramienta, definiendo un desfase en X de 139.17mm, un desfase en Z de 184.72mm y una rotación sobre el eje Y de 61.7°, valores obtenido gracias a la función snap object y seleccionar la punta de la herramienta:
 
![Creación Data Tool](/imagenes/robotStudio3.jpg)
![Creación Data Tool 2](/imagenes/robotStudio4.jpg)  
 
Luego se importa la geometría que contiene los perfiles de las letras y se modifica orientación y posicionamiento para ubicarlo de una forma óptima y que cumpla con ubicarse en el cuadrante X+ Y+.
 
Se generan las trayectorias al seleccionar los contornos de los perfiles y se les ajusta velocidad y zona.
 
Además se generaron 2 jointtarget para definir el home y un punto cercano al plano pero alejado, lo que permitió hacer sus respectivas rutinas agregándolas a un path de forma individual.
 
![Creación Jointtarget](/imagenes/robotStudio5.jpg)
 
 
 
## Resultados
### Videos
Tras el desarrollo del laboratorio se presentaron inconvenientes para ser completado en su totalidad, se cuenta con la simulación en RobotStudio (“SimulacionRobotStudio”) y una ejecución al aire del código (“VideoEjecucionAlAire”), vídeos alojados dentro del repositorio en la carpeta “Videos”. 
 
Su montaje en el robot articulado IRB 140 se puede visualizar en la siguiente figura:
![montaje](/imagenes/montaje.jpg)  
 
 
### Código RAPID
#### Código para trayectoria en plano inclinado a 45°.  
```rapid
MODULE Module1
        CONST robtarget Target_10:=[[-61.252986291,204.835773881,99.999999785],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_20:=[[-61.252986291,204.835773777,-0.000000215],[0,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_30:=[[-61.252986291,84.835773776,-0.000000089],[0,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_40:=[[-91.39885339,84.835773776,-0.000000089],[0,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_50:=[[-91.39885339,181.98326162,-0.000000191],[0,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_60:=[[-141.285401202,181.98326162,-0.000000191],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_70:=[[-141.285401202,204.835773777,-0.000000215],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_80:=[[-61.252986291,204.835773777,-0.000000215],[0,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_90:=[[-61.252986291,204.835773881,99.999999785],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_100:=[[-207.411819355,207.169647462,99.999999783],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_110:=[[-207.411819355,207.169647358,-0.000000217],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_120:=[[-164.526892288,190.832532285,-0.0000002],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_130:=[[-152.638723731,171.189096304,-0.00000018],[0.000000001,0.999944963,-0.010491487,0.000000001],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_140:=[[-148.676000878,144.933018508,-0.000000152],[0,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_150:=[[-164.575514654,99.471106029,-0.000000104],[-0.000000001,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_160:=[[-183.258658901,86.744201652,-0.000000091],[-0.000000001,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_170:=[[-207.509064087,82.501900194,-0.000000087],[0,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_180:=[[-231.334023568,85.516486904,-0.00000009],[-0.000000001,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_190:=[[-248.060117572,92.51810765,-0.000000097],[-0.000000001,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_200:=[[-248.060117572,121.108059027,-0.000000127],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_210:=[[-245.045530862,121.108059027,-0.000000127],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_220:=[[-232.014736696,111.189096305,-0.000000117],[0,0.999944963,-0.010491487,0.000000001],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_230:=[[-222.825109468,106.764460972,-0.000000112],[0,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_240:=[[-212.274055983,104.965433419,-0.00000011],[0,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_250:=[[-200.361576243,107.007572804,-0.000000112],[0.000000001,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_260:=[[-190.005012223,114.203683014,-0.00000012],[0.000000001,0.999944963,-0.010491487,0],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_270:=[[-182.663034914,126.602386417,-0.000000133],[0.000000001,0.999944963,-0.010491487,-0.000000001],[0,2,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_280:=[[-179.794315303,145.030263241,-0.000000152],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_290:=[[-182.760279646,163.847118995,-0.000000172],[-0.000000001,0.999944963,-0.010491487,-0.000000001],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_300:=[[-190.588480619,176.148577666,-0.000000185],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_310:=[[-200.993667004,182.712597115,-0.000000192],[-0.000000001,0.999944963,-0.010491487,0.000000001],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_320:=[[-212.468545449,184.706114133,-0.000000194],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_330:=[[-223.797556794,182.712597115,-0.000000192],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_340:=[[-240.037427134,173.279858055,-0.000000182],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_350:=[[-245.33726506,168.660733257,-0.000000177],[-0.000000001,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_360:=[[-248.060117572,196.861705705,-0.000000206],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_370:=[[-220.880214816,206.294444764,-0.000000216],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_380:=[[-207.411819355,207.169647358,-0.000000217],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST robtarget Target_390:=[[-207.411819355,207.169647462,99.999999783],[0,0.999944963,-0.010491487,0],[0,1,-2,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST jointtarget MyHome_LC:=[[0,0,0,0,30,0],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
    CONST jointtarget MyClose_LC:=[[0,25,20,170,15,-125],[9E+09,9E+09,9E+09,9E+09,9E+09,9E+09]];
!***********************************************************
    !
    ! Module:  Module1
    !
    ! Description:
    !   <Insert description here>
    !
    ! Author: user
    !
    ! Version: 1.0
    !
    !***********************************************************
    
    
    !***********************************************************
    !
    ! Procedure main
    !
    !   This is the entry point of your program
    !
    !***********************************************************
    PROC main()
        !Add your code here
        MyHomePath;
        MyClosePath;
        Letra_L;
        Letra_C;
        MyClosePath;
        MyHomePath;
    ENDPROC
    PROC Letra_L()
        MoveL Target_10,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_20,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_30,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_40,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_50,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_60,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_70,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_80,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_90,v200,z5,Marcador_LC\WObj:=Plano45;
    ENDPROC
    PROC Letra_C()
        MoveL Target_100,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_110,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_120,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_130,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_140,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_150,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_160,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_170,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_180,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_190,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_200,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_210,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_220,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_230,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_240,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_250,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_260,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_270,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_280,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_290,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_300,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_310,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_320,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_330,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_340,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_350,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_360,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_370,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_380,v200,z5,Marcador_LC\WObj:=Plano45;
        MoveL Target_390,v200,z5,Marcador_LC\WObj:=Plano45;
    ENDPROC
    PROC MyHomePath()
        MoveAbsJ MyHome_LC,v200,z5,Marcador_LC\WObj:=Plano45;
    ENDPROC
    PROC MyClosePath()
        MoveAbsJ MyClose_LC,v200,z5,Marcador_LC\WObj:=Plano45;
    ENDPROC
ENDMODULE
```
 
 
 
## Conclusiones
* La definición del Workobject permite trabajar sobre una superficie que pueda tener una disposición diferente a la determinada a través de RobotStudio. Gracias a este, se calibra la ubicación de los 3 puntos que los define y el plano de trabajo se adapta.
* Para el trabajo en RobotStudio es importante tener en cuenta las advertencias al generar las trayectorias, las cuales son reparadas al analizar y seleccionar la pose más conveniente según el movimiento y las posiciones clave que debe alcanzar.  
* La calibración manual de la herramienta con ayuda del brazo IRB 140 puede ser evitado si se cuenta con un completo y correcto modelado de la herramienta, ya que a través del software se define el TCP referente a la punta de la herramienta, sin embargo es recomendado realizar su calibración.    
* Es importante contar con un juego en el diseño de la herramienta, pues en caso de algún choque esta se retracte y evite algún inconveniente como dañar la máquina, le herramiento o golpear algún otro elemento.
 


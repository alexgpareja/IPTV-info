# IPTV
## Introducción

IPTV, que significa "Televisión por Protocolo de Internet" (en inglés, Internet Protocol Television), es una forma de distribución de señales de televisión a través de protocolos de Internet.
Hoy en día cada vez es más popular su uso, como alternativas a la tradicional TDT (ya que no es necesario tener ninguna antena parabólica, ni TV con entrada satélite. De hecho, ni televisión hace falta. Mientras se tenga conexión a internet, puedes ver los canales que quieras, ya sea en televisión, portátil, pc, móvil...

El motivo por el que hago esta guía es para ayudar a las personas que no entiendan o no sepan como funciona, pero sobre todo a aquellas personas más maniáticas y perfeccionistas como yo, que quieran configurar su propia lista, tener los canales en un orden en específico, con un nombre en concreto, un logo y un EPG vinculado correctamente. 

### Advertencias Legales

Es importante destacar que hay servicios legítimos de IPTV que ofrecen contenido legal y con licencia. Sin embargo, también hay servicios ilegales que ofrecen acceso a canales sin los derechos de autor necesarios. Se recomienda a los usuarios que utilicen servicios legítimos y respeten las leyes de derechos de autor y propiedad intelectual.

Por obvias razones, en esta guía yo no voy a ofrecer ningún link a ninguna lista que no sea legal, yo no tengo nada que ver en como tu hayas obtenido tu lista, ni si es legal o no.

### Conceptos Básicos

* IPTV: Internet Protocol Television
* M3U o M3U8: Listado para introducir en tu reproductor deseado. Usa este enlace si deseas utilizar cualquier aplicación IPTV genérica. Utiliza la M3U en caso que la M3U8 no te funcione. Cuando tu obtienes tu servicio iptv, te suele llegar un link muy largo que acabará en .m3u o en .m3u8. Es el formato de la lista iptv. .m3u es un formato de lista de reproducción más antiguo y general, mientras que .m3u8 se ha vuelto más común en el contexto de la Mi consejo es que primero pruebes .m3u8, y si tienes algún problema de incompatibilidad pues ya mires el .m3u.
* M3U8 + MPD: En pruebas Incluye los mismos canales que la M3U8, pero además los que emiten en formato MPD.
* ENIGMA2: Formato especial para el receptor Linux Enigma2.
* W3U: Formato especial para [Wiseplay](https://play.google.com/store/apps/details?id=com.wiseplay).
* EPG: "Electronic Program Guide" (Guía Electrónica de Programación) en inglés. Es un servicio que proporciona información sobre la programación de canales de televisión y radio. Lo que vendría siendo el teletexto de toda la vida, pero para nuestra lista.

### Fuentes de Contenido IPTV

Actualmente en España hay una iniciativa, dirigida por @LaQuay en la que se ofrecen diversos canales de la TDT española de forma LEGAL y GRATUITA. Podéis echar un vistazo aquí si os interesa saber más del tema, o conseguir vuestra primera lista IPTV.
https://github.com/LaQuay/TDTChannels

A nivel internacional, hay todo un github comunidad con información, listas gratuitas y legales, tutoriales, etc muy interesante también, eso si, está en inglés.
https://github.com/iptv-org/iptv

## Al recibir la lista
Supongamos que vuestro proveedor os ha enviado un mensaje similar a: 

Querido usuario, aquí tienes tu lista. 
Una url bastante larga que suele tener una forma similar a http://url del servidor . algo : 0000/get...username=usuario&password=contraseña...m3u8 (o algo así, depende de donde la conseguís puede ser diferente)

Xtream:
username=unlindonombredeusuario
password=completamentelegal
URL: una url

Nosotros nos centraremos en ese link largo, que al entrar en el suele descargarte un documento .m3u o .m3u8 al dispositivo en el que lo abres (a veces puede costar de descargar).

Entonces si intentamos abrir ese documento con doble-click seguramente se abra vuestro reproductor predeterminado (por ejemplo VLC, el del cono) y se reproduzca el primer canal de la lista.

Entonces nos encontramos con el primer problema, quizás no nos interesa tener +10.000 canales en 400 idiomas, quizás solo nos interesa tener los de España, y no necesariamente todos...

Vamos a ver como podemos arreglar esto.

## Editar lista de IPTV
Comentar que es algo que desaconsejo, yo dejaría la recibida como está, por si pasase cualquier cosa, te equivocas y borras algun link o lo que sea (Aunque siempre puedes volver a descargarla desde el link). Personalmente veo mejor que crees otro archivo .m3u8 desde 0 y entonces vayas copiando los canales que te interesan.

Sino, puedes editar directamente esa lista descargada (tampoco pasa nada) haciendo click derecho y abrir con Bloc de notas, Text Edit, Vscode, Notepad, etc...

## Estructura de M3U
La estructura de un archivo m3u debe contener una serie de etiquetas determinadas distribuidas en tres líneas.
La estructura es la siguiente:

`#EXTM3U`

`#EXTINF: (duración), (atributos),(título del canal)`

`URL`

EJEMPLO DE LO QUE TE PUEDES ENCONTRAR:

#EXTM3U

#EXTINF:-1 tvg-id="TVE", tvg-name="La 1", group-title="TDT", tvg-logo="https://www.movistarplus.es/recorte/m-NEO/canal/TVE.png", La 1

urldelcanalemitiendo

#EXTINF:-1 tvg-id="La2", tvg-name="La 2", group-title="TDT", tvg-logo="https://www.movistarplus.es/recorte/m-NEO/canal/TVE.png", La 2

urldelcanal2emitiendo

***


#EXTM3U
Etiqueta obligatoria y debe ir al principio del documento. Solo se escribe una única vez en todo el documento e indica a los reproductores que esa es una lista M3U Extendida. Es Extendida porque incluye atributos adicionales que no están presentes en una lista M3U básica.

#EXTINF:
Indica donde comienzan los metadatos adicionales de cada streaming. Debe usarse una línea para cada streaming incluido en la lista. Por ejemplo si listamos 5 canales de TV, habrá que crear 5 líneas #EXTINF:

duración
Indica la duración en segundos del archivo multimedia referenciado. En listas IPTV se usan dos parámetros. o bien 0 o bien -1. Ambos parámetros tienen la misma función, indican que la duración del streaming no es fija y no es posible determinarse. Algunos reproductores lo interpretan de forma ligeramente diferente, el parámetro 0 se refiere a una retransmisión almacenada en caché, y por lo tanto se puede hacer resumen de la retransmisión, esto es, hacer una pausa y continuar en el mismo punto donde se dejó. El parámetro -1 indica que es una retransmisión en vivo y no se puede hacer resumen.

Tras el parámetro de duración debe colocarse un espacio en blanco
Ejemplo: #EXTINF:-1 ,Nombre del canal

### **ATRIBUTOS**
Son una serie de etiquetas opcionales que añaden metadatos que pueden ser leídos por los reproductores. No todos los reproductores son capaces de interpretar todos los atributos.
Entre los atributos debe dejarse un espacio en blanco.
Existen varias etiquetas de atributos, pero las más usadas en listas IPTV son las siguientes:

**tvg-id=”ID EPG”**

Indica el ID o identificador de EPG o guía de programación. EPG (Electronic Program Guide) es similar al teletexto, ofrece la programación horaria de los diferentes canales de TV. En las retransmisiones de TV digital, aparte de los datos de video y audio, también se pueden enviar datos adicionales con la programación de ese canal. En IPTV esto no es posible y normalmente se ofrecen estas guías en formato XML que hay que descargar y usar de forma local, o bien descargar de una URL.

Si especificamos el ID de cada canal listado en la guía EPG, el reproductor mostrará la información de dicho canal. La forma de mostrar esta información difiere en cada reproductor. Por ejemplo, si utilizas siptv, en su web te dice los id de los canales para reconocerte automáticamente el epg. https://siptv.app/codes/
Intuyo que probablemente cada aplicación de IPTV player tendrá sus propios id, mejor comprovadlo en la web oficial de la app.

**tvg-name=”ID EPG”**

Especifica el nombre que va a recibir el canal de forma interna. No es el nombre que aparecerá en los reproductores. Suele usarse en vez de la etiqueta tvg-id="". Este nombre suele ser el que aparece en la guía EPG que muestran algunos reproductores. Si en nuestro archivo m3u se combinan las etiquetas tvg-id="" y tvg-name="" , el primero indica el ID del canal en la guía y el segundo es el nombre que se verá cuando se muestra la guía. Si solo se usa el parámetro tvg-name="", ese será el identificador en la guía EPG.

Otra forma en la que se puede asociar un determinado canal a su información EPG es que el nombre del canal debe ser exactamente el mismo que el de la lista EPG de dicho canal. Por ejemplo imagina que buscas en google lista epg España, y te la descargas (probablemente sea en formato .xml) pues si abres el documento ahí verás que cada canal tiene un nombre escrito de una forma única, tienes que tenerlo igual para que se asocie ese canal al de tu lista .m3u8.

Ejemplo:
#EXTINF:-1 , tvg-id="La 1" ,La 1 HD
#EXTINF:-1 , tvg-name="La 1" ,LA 1

**group-title=”Nombre de Grupo”**

Este parámetro indica el grupo o categoría del canal. Puede que queramos agrupar los diferentes canales en categorías, por ejemplo Películas, Culturales, Infantiles, etc…
Algunos reproductores permiten agrupar los canales por categorías y con este parámetro podremos indicarle a que categoría pertenece cada canal.

**tvg-logo=”URL del LOGO”**

Este parámetro permite especificar la ruta a un logo que identifique al canal. Algunos reproductores son compatibles con este parámetro y muestran una imagen o logo que representa a cada canal. No todos los reproductores son compatibles con este parámetro.

**tvg-shift=ajuste**

Este es un ajuste para los horarios de la guía EPG. Es posible que la guía EPG usada no esté ajustada a tu horario. Con este parámetro podremos reajustar ese dato. Siempre debe tener los signos + ó -.
Este parámetro se coloca tras la etiqueta inicial #EXTM3U y tras un espacio en blanco.

Ejemplo:
#EXTM3U tvg-shift=+2

**audio-track="IDIOMA"**

Con este parámetro podemos especificar el o los idiomas de audio de los que consta el streaming. Los idiomas se deben especificar usando los códigos de idioma ISO 639-2. Si nuestro streaming tiene varios idiomas de audio disponibles, podemos especificarlos todos usan comas como separador. Algunos reproductores leen este parámetro y nos muestra los idiomas disponibles para el canal que estamos reproduciendo.

Ejemplos:
#EXTINF:-1 tvg-logo="mega.png" group-title="España" audio-track="spa",MEGA
#EXTINF:-1 tvg-logo="mega.png" group-title="España" audio-track="spa,rus,eng",MEGA

### Título del canal
Aquí indicaremos el nombre que aparecerá en los reproductores. debe ir precedido de una coma. Es literalmente el nombre que tu verás en tu aplicación cuando estás haciendo zaping y sale el recuadrito abajo indicandote el canal en el que estas. Puedes llamar al canal como quieras.

Ejemplos:
#EXTINF:-1 tvg-logo="mega.png" group-title="España",MEGA
#EXTINF:-1 tvg-logo="mega.png" group-title="España",Mega
#EXTINF:-1 tvg-logo="mega.png" group-title="España",MEGA FHD
#EXTINF:-1 tvg-logo="mega.png" group-title="España",MEGA HD


(Esto es muy útil si tienes el mismo canal, pero en diferentes resoluciones).

### URL del Canal
Y finalmente la URL del canal donde está emitiendo. 


## Plantilla editable
https://github.com/alexgpareja/IPTV-info/blob/main/Plantilla_Iptv.m3u8

# EPG

Perfecto, ya tengo mi lista de canales IPTV a mi gusto, ordenada como quiero y sin mil canales que no me interesan, pero no me sale la guía, quiero saber que estan dando en cada canal...

Eso es por que falta configurar correctamente el EPG. Puede ocurrir que depende de donde obtengas la lista no te venga ningún EPG, o solo de algunos canales. Vamos a ver como podemos configurarla.

## Crear mi propia EPG

Aquí lo cierto es que no puedo ayudar demasiado, ya que no he se bien como crear una propia. El problema de las listas EPG es que aun que sean archivos XML, tienes que configurarlas para que cada cierto tiempo vayan actualizando los datos de los programas a emitir, para eso es necesario instalar cosas, etc

Si quieres investigar más sobre el tema, prueba a buscar acerca de Webgrabplus, o en https://github.com/iptv-org/epg también puedes ver como crear un mini programa con nodejs para obtener los datos de las guias. 

## De donde saco la información de la programación

Existen varias páginas en las que puedes ver la programación diaria de los canales de televisión. Por lo personal yo recomiendo la de https://www.movistarplus.es/programacion-tv ya que tiene todos los canales de España que nos suelen interesar. (También saco de aquí las url de las fotos de cada canal).

## Utilizar EPG de internet

Está es la opción más fácil y viable si no quieres instalar nada ni tener que ir toqueteando. Pero si nadie te explica puede parecerte algo complicado, sobre todo si después de cargar la guía resulta que sigue sin aparecer la info de los canales (problema que me ocurrió a mi).

Cual es la solución (que parece funcionar)? Pues es más fácil de lo que parece. Os acordais cuando anteriormente creando la lista IPTV poniamos un atributo llamado _**tvg-id**_. Bien, pues este id tiene que ser igual (tocará editarlo en nuestra lista probablemente) al id que aparece en la lista EPG. 

La estructura del EPG es la siguiente:

`<?xml version="1.0" encoding="UTF-8"?>`

`<tv generator-info-name="WebGrab+Plus/w MDB &amp; REX Postprocess -- version V2.1.11.0 -- Jan van Straaten" generator-info-url="http://www.webgrabplus.com">`

  `<channel id="LA 1">`
    `<display-name lang="es">LA 1</display-name>`
    `<icon src="https://www.movistarplus.es/recorte/m-NEO/canal/TVE.png" />`
    `<url>http://www.movistarplus.es</url>`
  `</channel>`

Pues esa etiqueta: channel id="LA 1", es la que nos indica el id que debe tener el canal en nuestra lista iptv. (Por si acaso yo también lo pongo igual en el tvg-name, aunque no debería ser necesario).

## Algunas listas EPG actualizadas

https://raw.githubusercontent.com/dracohe/CARLOS/master/guide_IPTV.xml (yo ando usando esta)
https://raw.githubusercontent.com/dracohe/SMARTIPTV/master/guide.xml

Podeis mirar más aquí: https://www.pluginsxbmc.com/2019/10/guias-epg-actualizadas.html

# Webgrafia y fuentes

https://github.com/iptv-org/epg
https://github.com/LaQuay/TDTChannels
https://www.lonasdigital.com/threads/estructura-de-una-lista-m3u-para-iptv.73021/
https://www.movistarplus.es/programacion-tv
https://www.pluginsxbmc.com/2019/10/guias-epg-actualizadas.html
https://raw.githubusercontent.com/dracohe/CARLOS/master/guide_IPTV.xml

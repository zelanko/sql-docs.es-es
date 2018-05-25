---
title: Notas de la versión de SQL Operations Studio (versión preliminar) | Documentos de Microsoft
description: Notas de la versión de SQL Operations Studio (versión preliminar)
ms.custom: tools|sos
ms.date: 05/08/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f461b78c3d76f7e6b848b83d8a2333dffe5de3c
ms.sourcegitcommit: a9da0abd3e17fbcd6339980d7331d0418cdada53
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/24/2018
---
# <a name="sql-operations-studio-preview-release-notes"></a>Notas de la versión de SQL Operations Studio (versión preliminar)

**[Descargue la versión preliminar pública de mayo](download.md)**


## <a name="may-2018-may-public-preview"></a>De 2018 de mayo (mayo de vista previa pública)

fecha de lanzamiento: 7 de mayo de 2018  
versión: 0.29.3

El *puede Public Preview* se centra en la estabilización y correcciones de errores. Esta compilación que contiene los puntos principales siguientes:  

- Informe sobre la ampliación de la búsqueda de SQL Redgate disponible en el Administrador de extensiones.
- Localización de la Comunidad disponible en 10 idiomas: alemán, español, francés, italiano, japonés, coreano, portugués, ruso, chino simplificado y chino tradicional.
- Recopilación de telemetría reducida, una mejor experiencia de desactivación y vínculos del producto a la declaración de privacidad.
- Administrador de extensiones tiene Marketplace mejor experiencia para descubrir fácilmente las extensiones de la Comunidad.
- Extensión trabajos del Agente SQL y el historial de trabajos para la mejora de vista.
- Actualizaciones de whoisactive y extensiones de informes del servidor.
- Mejorar el desplazamiento de administrar propiedades de panel.
- Solucionar problemas de GitHub:
   - Corregir [emitir 703](https://github.com/Microsoft/sqlopsstudio/issues/703): escribir texto similar a HTML en los datos de edición hace el valor no se muestran correctamente hasta que la actualización
   - Corregir [emitir 821](https://github.com/Microsoft/sqlopsstudio/issues/821): dependencia del paquete sqlopsstudio.deb
   - Corregir [emitir 1260](https://github.com/Microsoft/sqlopsstudio/issues/1260): palabra clave 'distinct' no resaltado
   - Corregir [emitir 1332](https://github.com/Microsoft/sqlopsstudio/issues/1332): editar datos revertir fila no funciona
   - Corregir [emitir 1215](https://github.com/Microsoft/sqlopsstudio/issues/1215): extensión del Agente SQL y la barra de estado
   - Corregir [emitir 1316](https://github.com/Microsoft/sqlopsstudio/issues/1316): cambiar el tamaño no de agente SQL después de cambiar el tamaño de windows


Para obtener más información, consulte el [registro de cambios](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md), y [versiones](https://github.com/Microsoft/sqlopsstudio/releases).



## <a name="april-2018-april-public-preview"></a>Abril de 2018 (versión preliminar pública de abril)

fecha de lanzamiento: 25 de abril de 2018  
versión: 0.28.6

El *abril Public Preview* contiene mejoras y correcciones de errores. 

- Mejoras en la extensión de la versión preliminar del Agente SQL.
- Grandes y protegido el archivo compatibilidad mejorada para guardar administrador protegida y > 256M archivos dentro de las operaciones de SQL Studio.
- Integra la división de Terminal para trabajar con varias terminales abiertos al mismo tiempo.
- Imprimir en el pie de recuento de archivo en disco de instalación reducido para instalaciones más rápidas y tiempos de inicio.
- Seguir solucionar problemas de GitHub:
   - Corregir [emitir 37](https://github.com/Microsoft/sqlopsstudio/issues/37): cuando el Visor gráfico produce un error, se produce un comportamiento inesperado.
   - Corregir [emitir 462](https://github.com/Microsoft/sqlopsstudio/issues/462): solicitud de característica: opción para grupos de servidores se expanda de forma predeterminada.
   - Corregir [emitir 606](https://github.com/Microsoft/sqlopsstudio/issues/606): intellisense - propuesta no válida para el comando 'update'.
   - Corregir [emitir 967](https://github.com/Microsoft/sqlopsstudio/issues/967): esperar que el plan de consulta cuando selecciona el plan de presentación XML en la cuadrícula de resultados.
   - Corregir [emitir 1023](https://github.com/Microsoft/sqlopsstudio/issues/1023): agregar corchetes para llamada ms_foreachdb desde flyfishingdba.
   - Corregir [emitir 1048](https://github.com/Microsoft/sqlopsstudio/issues/1048): error de protocolo de enlace de inicio de sesión previo SSL/TLS.
   - Corregir [emitir 1050](https://github.com/Microsoft/sqlopsstudio/issues/1050): visión clara ver antes de mostrar el error.
   - Corregir [emitir 1057](https://github.com/Microsoft/sqlopsstudio/issues/1057): nuevas acciones de consulta en el Explorador de widget y restauración se interrumpen.
   - Corregir [emitir 1068](https://github.com/Microsoft/sqlopsstudio/issues/1068): panel Salida pop-up windows con el mensaje de error para la base de datos de SQL Azure.
   - Corregir [emitir 1069](https://github.com/Microsoft/sqlopsstudio/issues/1069): error de servidor necesario cuando se muestra inicialmente se muestra el cuadro de diálogo de conexión.
   - Corregir [emitir 1070](https://github.com/Microsoft/sqlopsstudio/issues/1070): grupos de servidores requieren ahora un doble clic para expandir.
   - Corregir [emitir 1072](https://github.com/Microsoft/sqlopsstudio/issues/1072): fondo del control de selección es semitransparente.
   - Corregir [emitir 1115](https://github.com/Microsoft/sqlopsstudio/issues/1115): Corregir contraste alto todos los problemas de accesibilidad en Studio de operaciones de SQL.
   - Corregir [emitir 1101](https://github.com/Microsoft/sqlopsstudio/issues/1101): se produce un error de extensión para la actualización "descargar manualmente" vínculo llega a una ubicación incorrecta.
   - Corregir [emitir 1103](https://github.com/Microsoft/sqlopsstudio/issues/1103): desplazamiento V no está trabajando en la ficha Inicio.
   - Corregir [emitir 1104](https://github.com/Microsoft/sqlopsstudio/issues/1104): fichas de la extensión SQL dejó de funcionar.


Un hito significativo para la versión preliminar pública de abril es la actualización de código de origen de plataforma 1.21 de código de Visual Studio. De esta forma, en algunas actualizaciones para el editor principal y el área de trabajo desde el punto de 1.19 sincronización anterior. Algunos ejemplos incluyen lo siguiente:

- [Nueva interfaz de usuario de las notificaciones](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui) : administrar fácilmente y revisar las notificaciones de las operaciones de SQL Studio.
- [Integra dividir Terminal](https://code.visualstudio.com/updates/v1_21#_split-terminals) -trabajar con varias terminales abiertos al mismo tiempo.
- [Guardar archivos de gran tamaño y protegidos](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges) : guarda administrador protegida y > 256 M archivos dentro de las operaciones de SQL Studio.
- [Mejora la compatibilidad con archivos grandes](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements) -optimizaciones de búfer de texto para archivos de gran tamaño.
- [Búsqueda de configuraciones mejorada](https://code.visualstudio.com/updates/v1_20#_settings-search) - fácil encontrar el valor derecho con búsqueda en lenguaje natural.
- [Fragmentos de código globales](https://code.visualstudio.com/updates/v1_20#_global-snippets) -crear fragmentos de código que se puede usar en todos los tipos de archivo.
- [Selección múltiple de explorador](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer) -realizar acciones en varios archivos a la vez.
- [Errores y advertencias en el Explorador de](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer) : rápidamente ir a los errores en la base de código.
- [Arrastre & Quitar, copiar y pegar entre windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support) -mover archivos a través de ventanas abiertas de SQL Studio de operaciones.
- [Compatibilidad de submódulo GIT](https://code.visualstudio.com/updates/v1_20#_git-submodules) -Git realizar operaciones en repositorios Git anidados.
- [Soporte técnico de lector de pantalla del Terminal](https://code.visualstudio.com/updates/v1_20#_screen-reader-support) -Terminal integrado tiene ahora el modo de "Pantalla lector optimizado".
- [Diseño centrado editor](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout) -maximizar su código ver espacio real en pantalla.
- [Resultados de la búsqueda horizontal (versión preliminar)](https://code.visualstudio.com/updates/v1_21#_horizontal-search) -puede ahora ver los resultados en un panel horizontal.

Para obtener más detalles, desprotección la [notas de versión de febrero de código de Visual Studio](https://code.visualstudio.com/updates/v1_21)y el [notas de versión de enero de código de Visual Studio](https://code.visualstudio.com/updates/v1_20).

Para obtener más información, consulte el [registro de cambios](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md).

## <a name="march-2018-march-public-preview"></a>De 2018 de marzo (vista previa pública de marzo)

fecha de lanzamiento: 28 de marzo de 2018  
versión: 0.27.3

El *marzo Public Preview* continúa solucionar los problemas de GitHub superiores y se concentra en mejorar nuestra historia de extensibilidad. Habilitar específicamente el Administrador de extensiones, mejora la administración de panel y proporcionar el Agente SQL y las extensiones de visión. Esta versión incluye las siguientes mejoras:

- Mejorar el modelo de extensibilidad de panel para admitir la visión con fichas y paneles de configuración.
   - Administrador de extensiones permite simple adquisición de extensiones.
   - Extensiones de panel para sp_whoisactive de [whoisactive.com](http://www.whoisactive.com).
   - Para obtener más información, consulte [ampliar la funcionalidad de las operaciones de SQL Studio](extensions.md).
- Agregar más [API de extensibilidad para la conexión y el objeto explorer](https://github.com/Microsoft/sqlopsstudio/wiki/Extensibility-API) administración.
- Prosiga para arreglar afecta a los clientes importantes [GitHub problemas](https://github.com/Microsoft/sqlopsstudio/issues).


## <a name="february-2018-february-public-preview"></a>Febrero de 2018 (vista previa pública de febrero)

fecha de lanzamiento: 15 de febrero de 2018  
versión: 0.26.7

El *Public Preview de febrero* incluye algunas sugerencias sobre características y correcciones de errores de alta prioridad. Esta versión incluye las siguientes mejoras:

- Introducción a la instalación de actualizaciones automáticas, que proporciona una notificación cuando una nueva versión está disponible para descargar 
- El campo de cuadro de diálogo de conexión 'Database' es ahora una lista de desplegable completa dinámicamente que contendrá una lista de bases de datos que se rellenan desde el servidor especificado.
- Corregir [emitir 6](https://github.com/Microsoft/sqlopsstudio/issues/6): mantener la conexión y la base de datos seleccionada al abrir nuevas pestañas de consulta.
- ¿Corregir [emitir 22](https://github.com/Microsoft/sqlopsstudio/issues/22): 'NombreDeServidor' y 'Nombre de la base de datos' - estos pueden ser listas desplegables en lugar de cuadros de texto?
- Corregir [emitir 549](https://github.com/Microsoft/sqlopsstudio/issues/549): instalación silenciosa de silenciosa/muy da como resultado de la aplicación que abre después de la instalación.
- Corregir [emitir 481](https://github.com/Microsoft/sqlopsstudio/issues/481): agregar la opción "Buscar actualizaciones".
- Colores del Editor SQL y las correcciones de finalización automática:
   - Corregir [emitir 584](https://github.com/Microsoft/sqlopsstudio/issues/584): palabra clave "Completa" no resaltada por IntelliSense.
   - Corregir [emitir 345](https://github.com/Microsoft/sqlopsstudio/issues/345): funciones de colorear SQL en el editor.
   - Corregir [emitir 300](https://github.com/Microsoft/sqlopsstudio/issues/300): [#tempData] más reciente "]" se mostrará de color verde.
   - Corregir [emitir 225](https://github.com/Microsoft/sqlopsstudio/issues/225): error de coincidencia de color de palabra clave.
   - Corregir [emitir 60](https://github.com/Microsoft/sqlopsstudio/issues/60): sql no válido color resaltado de sintaxis cuando se usa una tabla temporal en cláusula from.
- Introducir la API de extensibilidad de conexión.
- Integración de VS 1.19 del Editor de código.
- Actualizar componentes JustinPealing/html--plan de consulta para la recogida varias mejoras del Visor de Plan de consulta.


## <a name="january-2018-january-public-preview"></a>Enero de 2018 (vista previa pública de enero)

fecha de lanzamiento: 17 de enero de 2018  
versión: 0.25.4

El *Public Preview de enero* incluye algunas sugerencias sobre características y correcciones de errores de alta prioridad. Esta versión incluye las siguientes mejoras:

- Conexiones de servidor guardadas están disponibles en el cuadro de diálogo de conexión.
- Habilitar salida activa. Salida activa está desactivada de forma predeterminada, para habilitar vea [configuración de salida activa](settings.md#hot-exit).
- En función de grupo de servidores de sintaxis de pestaña. Color de la ficha está desactivada de forma predeterminada, para habilitar vea [ficha Configuración de color](settings.md#tab-color).
- Cambio *nombre del servidor* a *Server* en el cuadro de diálogo de conexión.
- Arreglado roto *ejecutar la consulta actual* comando.
- Corregir errores de secuencias de comandos de separación de arrastrar y colocar.
- Corregir incorrectos de los iconos anclados menú Inicio.
- Corregir falta la cuenta de Azure icono de personalización de marca.


## <a name="december-2017-december-public-preview"></a>Diciembre de 2017 (vista previa pública de diciembre)

fecha de lanzamiento: 19 de diciembre de 2017  
versión: 0.24.1

El *diciembre Public Preview* incluye varias correcciones de errores en todas las áreas de características, así como a las siguientes mejoras:

- Crear cuadro de diálogo de regla de Firewall ya está disponible para ayudar a conectarse a la base de datos de SQL Azure y almacenamiento de datos de SQL Azure.
- Ha agregado el programa de instalación de Windows y los paquetes de instalación de Linux DEB y RPM.
- Administrar el editor de diseño visual de panel.
- *Secuencia de comandos como Alter* y *como ejecutar Script* comandos.
- *Ejecutar la consulta actual con el Plan real* comando.
- Integrar la plataforma de editor de código de VS 1.18.1.
- Habilitar los archivos de instalación de prueba de extensión VSIX.
- Admite la sintaxis de iteración de lote "Vaya N".


## <a name="november-2017"></a>Noviembre de 2017

fecha de lanzamiento: 15 de noviembre de 2017  
versión: 0.23.6

- Versión de inicial [!INCLUDE[name-sos](../includes/name-sos-short.md)].


## <a name="next-steps"></a>Pasos siguientes

Vea uno de los tutoriales siguientes para empezar a trabajar:
- [Conectar & consultas SQL Server](quickstart-sql-server.md)
- [Conectarse y consultar la base de datos SQL Azure](quickstart-sql-database.md)
- [Conectarse y consultar el almacenamiento de datos de Azure](quickstart-sql-dw.md)

Contribuir a [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio)

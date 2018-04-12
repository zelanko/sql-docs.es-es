---
title: Notas de la versión de SQL Operations Studio (versión preliminar) | Documentos de Microsoft
description: Notas de la versión de SQL Operations Studio (versión preliminar)
ms.custom: tools|sos
ms.date: 03/28/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba86403e791af25de4f7bcd8b1cbd7b5f188897b
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="sql-operations-studio-preview-release-notes"></a>Notas de la versión de SQL Operations Studio (versión preliminar)

**[Descargue la versión preliminar pública de marzo](download.md)**

## <a name="march-2018-march-public-preview"></a>De 2018 de marzo (vista previa pública de marzo)

fecha de lanzamiento: 28 de marzo de 2018  
versión: 0.27.3

El *marzo Public Preview* continúa solucionar los problemas de GitHub superiores y se concentra en mejorar nuestra historia de extensibilidad. Habilitar específicamente el Administrador de extensiones, mejora la administración de panel y proporcionar el Agente SQL y las extensiones de visión. Esta versión incluye las siguientes mejoras:

- Mejorar el modelo de extensibilidad de panel para admitir la visión con fichas y paneles de configuración.
   - Administrador de extensiones permite simple adquisición de extensiones.
   - Extensiones de panel para sp_whoisactive de [whoisactive.com](http://www.whoisactive.com).
   - Para obtener más información, consulte [ampliar la funcionalidad de las SQL Operations Studio](extensions.md).
- Agregar más [API de extensibilidad para la conexión y el objeto explorer](https://github.com/Microsoft/sqlopsstudio/wiki/Extensibility-API) administración.
- Prosiga para arreglar afecta a los clientes importantes [GitHub problemas](https://github.com/Microsoft/sqlopsstudio/issues).

Para obtener más información, consulte el [registro de cambios](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md).


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

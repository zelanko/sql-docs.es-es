---
title: Notas para (SSRS) 2017 y versiones posteriores de la versión | Microsoft Docs
ms.date: 09/01/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.reviewer: maghan
author: casualoak
ms.author: RhysSchmidtke
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: c85d3811fc467d94dc1841b871964e3bb594e2df
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58283302"
---
# <a name="release-notes-for-sql-server-reporting-services-ssrs-2017-and-later"></a>Notas de la versión de SQL Server Reporting Services (SSRS) 2017 y versiones posteriores

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)]

En este artículo se describe los cambios en [!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS), para las versiones 2017 y versiones posteriores.

Para las notas para los controles de Visor de informes, vea [notas de la versión para el Visor de informes los controles de formularios Web Forms y formularios Windows Forms de SSRS](application-integration/release-notes-ssrs-application-integration.md).

<!--
We are "standardizing" all our 'Release Notes' style articles:

  - File names:   'release-notes-[TechArea-Name].md'


  - Content format:   2-column tables.  No longer using bullet lists.

    - Ideally, the 'Details' column should contain a link to another SSRS documentation article wherein the particular issue fix is discussed in any way.  Or if there is more to say beyond one sentence, the other sentences of elaboration would go into the 'Details' column.


  - H2 header names are kept short, for better display.


  - Try to keep all Release Notes in one .md file.  Avoid having multiple R.N. files whose names differ only by version or date.

    - Seriously consider erasing info about ancient releases that are so old that nobody cares about them anymore.  If you really want to retain ancient info, consider doing so in an HTML comment at the end of the .md file, just in case a Microsoft employee needs to re-examine ancient info.  In any case, this file cannot get ever longer, and some deletion or hiding of oldest info must eventually occur.


  - Do use '::: moniker range=' zones when version 2017 is no longer the only version represented inside this .md file.

    - Use the '=' operator on the moniker, not the '>=' operator.
    - In contrast, in our 'Whats New' articles we do use the '>=', rather than '='.

GeneMi, DevOps = 1467988 (MsEng > TechnicalContent) , 2019/03/19
-->

## <a name="1406001109-20190212"></a>14.0.600.1109, 2019/02/12

| Se corrigió un problema | Detalles |
| :---------- | :------ |
| El almacenamiento en caché de las programaciones de instantáneas de informes cambia a "Programación específica del informe" tras modificar la suscripción. | &nbsp; |
| rc:Toolbar=false no funciona en la edición Express. | &nbsp; |
| Algunos caracteres tailandeses se representan de forma incorrecta al exportar informes paginados a PDF. | &nbsp; |
| Interbloqueo durante la notificación de suscripciones controladas por datos. | &nbsp; |
| Las imágenes insertadas no se muestran en determinadas circunstancias cuando se usa el parámetro rc:Toolbar=False. | &nbsp; |
| No se pueden crear suscripciones controladas por datos para informes que usan parámetros en cascada. | &nbsp; |
| No se pueden editar suscripciones configuradas con un intervalo no válido. | &nbsp; |
| Actualizaciones de seguridad. | &nbsp; |
| No se muestra la interfaz de usuario de los informes vinculados. | &nbsp; |
| Algunos informes paginados con controles Tablix anidados tienen fuentes incorrectas. | &nbsp; |
| Espacio en blanco incorrectamente se agrega a determinados informes paginados que contienen regiones de datos tablix. | &nbsp; |
| Las filas de encabezado desaparecen al expandir las cuadrículas de datos simples de un informe móvil. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600906-20180912"></a>14.0.600.906, 2018/09/12

Se corrigió el problema siguiente:

| Se corrigió un problema | Detalles |
| :---------- | :------ |
| La autenticación personalizada no devuelve información de cookies correcta. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600892-20180831"></a>14.0.600.892, 2018/08/31

| Se corrigió un problema | Detalles |
| :---------- | :------ |
| El cuadro de texto dentro del rectángulo hace que el rectángulo no crezca verticalmente si rc:Toolbar=False y tiene texto largo. | &nbsp; |
| El tamaño del texto no se escala si pageHeight es inferior a 0,5 pulgadas. | &nbsp; |
| Se produce interbloqueo en la base de datos de catálogos SSRS cuando se usa con CRM. | &nbsp; |
| Encabezados de columna alineados de manera vertical mostrados de forma incorrecta al desplazarse hasta el informe. | &nbsp; |
| Los usuarios agregados al rol de informes SCOM tienen bloqueado el acceso al portal web de SSRS. | &nbsp; |
| Caracteres tailandés no se exportan correctamente en el archivo PDF. | &nbsp; |
| Cambio de comportamiento del rol Explorador. | &nbsp; |
| rc:Toolbar=false no funciona en la edición Express. | &nbsp; |
| Falta la barra de desplazamiento vertical en el área de mensajes de parámetros. | &nbsp; |
| Tiempo de ejecución de informes móviles actualizado. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600744-20180425"></a>14.0.600.744, 2018/04/25

| Se corrigió un problema | Detalles |
| :---------- | :------ |
| La página Suscripción controlada por datos no muestra la opción de entrega una vez creada. | &nbsp; |
| La actualización de SSRS 2012 a SSRS 2017 tiene como resultado que RSManagement lanza una excepción cada pocos segundos. | &nbsp; |
| No se pueden modificar los valores predeterminados para parámetros de varios valores en IE11. | &nbsp; |
| Los horarios están vacíos cada vez que se ejecuta una programación compartida. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600689-20180228"></a>14.0.600.689, 2018/02/28

| Se corrigió un problema | Detalles |
| :---------- | :------ |
| La visibilidad del parámetro de informe de un informe vinculado se revierte después de editar sus propiedades. | &nbsp; |
| El parámetro de la dirección URL rc:Toolbar=false no funciona en la edición Express. | &nbsp; |
| Tener expresiones en un cuadro de texto con el CanGrow propiedad se establece en false, se producirá en los valores que no se están mostrando. | &nbsp; |
| Se agregó el vínculo _Más información_ para la clave de producto en la configuración. | &nbsp; |
| El portal web con autenticación de formularios personalizados omite el deslizamiento de la cookie de expiración. | &nbsp; |
| Exportar a Word crea un alto de fila desigual si el contenido de la fila está vacío. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600594-20180109"></a>14.0.600.594, 2018/01/09

Algunas actualizaciones de seguridad se implementaron.

### <a name="140600490-20171101"></a>14.0.600.490, 2017/11/01

Problemas resueltos con la actualización de SKU.

## <a name="140600451-20170930"></a>14.0.600.451, 2017/09/30

Versión inicial.

## <a name="next-steps"></a>Pasos siguientes

[Novedades de Reporting Services (SSRS)](what-s-new-in-sql-server-reporting-services-ssrs.md)

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).

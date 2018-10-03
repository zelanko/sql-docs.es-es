---
title: Consideraciones administrativas para los publicadores de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], administrative considerations
- administering replication, Oracle publishing
ms.assetid: cfd81fb5-419b-4a1b-97c4-be7c9d4ee289
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9b46cca225d0c5abdb912910ee7bb9849c81c831
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48050481"
---
# <a name="administrative-considerations-for-oracle-publishers"></a>Consideraciones administrativas para los publicadores de Oracle
  Después de configurar un publicador de Oracle y de implementar los mecanismos de seguimiento de cambios de la replicación, los administradores del sistema de bases de datos de Oracle pueden seguir utilizando las utilidades estándar de bases de datos de Oracle y realizar las tareas normales de administración del sistema. No obstante, debe tener en cuenta los efectos de ciertas tareas administrativas sobre los datos publicados.  
  
 Excepto cuando se quita o se modifica una columna publicada para replicación, o cuando se quitan o se modifican objetos de replicación, estas consideraciones no se aplican a las publicaciones de instantáneas.  
  
## <a name="importing-and-loading-data"></a>Importar y cargar datos  
 Los desencadenadores se utilizan en el seguimiento de cambios para las publicaciones transaccionales en Oracle. Los cambios en las tablas publicadas solo se pueden replicar en los suscriptores si los desencadenadores de la replicación se activan al producirse una actualización, una inserción o una eliminación. Las utilidades Oracle Import y SQL*Loader de Oracle tienen opciones que determinan si un desencadenador se activará cuando se inserten filas en las tablas replicadas con estas utilidades.  
  
### <a name="oracle-import"></a>Oracle Import  
 Con Oracle Import, puede establecer la opción **ignore** en 'y' o 'n' (el valor predeterminado es 'n'). Si **ignore** se establece en 'n', la tabla se quita y se vuelve a crear durante la importación. Esto quita los desencadenadores de la replicación y deshabilita la replicación. Si **ignore** se establece en 'y', la importación intentará cargar las filas en la tabla existente, lo que activará los desencadenadores de la replicación. Por lo tanto, asegúrese de que **ignore** esté establecido en 'y' al importar en una tabla replicada con la herramienta Import.  
  
### <a name="sqlloader"></a>SQL*Loader  
 Con SQL\*Loader, puede establecer la opción **direct** en "true" o "false" (el valor predeterminado es "false"). Si **direct** se establece en 'false', las filas se insertan por medio de instrucciones INSERT convencionales, que activan los disparadores de la replicación. Si **direct** se establece en 'true', se optimiza la carga y no se activan los desencadenadores. Por lo tanto, asegúrese de que **direct** esté establecido en 'false' al cargar en una tabla replicada con la herramienta SQL*Loader.  
  
## <a name="making-changes-to-published-objects"></a>Realizar cambios en objetos publicados  
 Las siguientes acciones no requieren ninguna consideración especial:  
  
-   Volver a crear índices en tablas publicadas  
  
-   Agregar desencadenadores de usuario a una tabla publicada  
  
 La siguiente acción requiere que se detenga toda la actividad en las tablas publicadas:  
  
-   Mover una tabla publicada  
  
 Las siguientes acciones requieren que se quite la publicación, se lleve a cabo la operación y después se vuelva a crear la publicación:  
  
-   Truncar una tabla publicada  
  
-   Cambiar el nombre de una tabla publicada  
  
-   Agregar una columna a una tabla publicada  
  
-   Quitar o modificar una columna publicada para replicación  
  
-   Realizar operaciones no registradas  
  
## <a name="dropping-or-modifying-replication-objects"></a>Quitar o modificar objetos de replicación  
 Debe quitar y volver a configurar el publicador si quita o modifica cualquier tabla de seguimiento, desencadenador, secuencia o procedimiento almacenado de nivel de publicador. Para obtener una lista parcial de estos objetos, consulte [Objetos creados en el publicador de Oracle](objects-created-on-the-oracle-publisher.md).  
  
 Para obtener información acerca de cómo quitar y volver a configurar el publicador, vea la sección sobre la realización de cambios que requieren volver a configurar el publicador en el tema [Troubleshooting Oracle Publishers](troubleshooting-oracle-publishers.md).  
  
## <a name="see-also"></a>Vea también  
 [Configurar un publicador de Oracle](configure-an-oracle-publisher.md)   
 [Consideraciones y limitaciones de diseño de los publicadores de Oracle](design-considerations-and-limitations-for-oracle-publishers.md)   
 [Información general de la publicación de Oracle](oracle-publishing-overview.md)  
  
  

---
title: Seleccionar tablas y vistas de origen (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 479cc0e650c598e0a253caca796b854dc4eb69cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892673"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Seleccionar tablas y vistas de origen (Asistente para importación y exportación de SQL Server)
  Use la **seleccionar tablas de origen y las vistas** página para especificar las tablas y vistas para copiarse desde el origen de datos en el destino.  
  
> [!NOTE]  
>  No es necesario copiar todas las columnas en una tabla al seleccionar la opción de copia de tabla. Después de seleccionar una tabla de destino, haga clic en Editar asignaciones para mostrar el **asignaciones de columnas** cuadro de diálogo. Seleccione  **\<omitir >** en el **destino** columna de la **asignaciones de columnas** cuadro de diálogo para las columnas que desea omitir.  
  
 Para obtener más información acerca de este asistente, vea [Asistente para importación y exportación de SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información sobre las opciones para iniciar el asistente y sobre los permisos necesarios para ejecutar el asistente correctamente, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opciones  
  
### <a name="tables-and-views-list"></a>Lista de tablas y vistas  
 **Source**  
 Utilice las casillas para seleccionar en la lista las tablas y vistas disponibles que deben copiarse en el destino. Si selecciona una tabla o una vista de origen y no realiza ninguna otra acción, copiará el esquema y los datos del origen sin cambios.  
  
 **Destino**  
 Seleccione una tabla de destino de la lista para cada tabla de origen.  
  
> [!NOTE]  
>  Si interrumpe el asistente en este punto para crear una tabla de destino en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o con otra herramienta, la nueva tabla no será visible de forma inmediata en la lista de tablas de destino disponibles. Para actualizar la lista de tablas de destino, retroceda a la **elegir un destino** página, vuelva a seleccionar la base de datos de destino y, a continuación, avanzar paso a paso a la **seleccionar tablas de origen y las vistas**.  
  
### <a name="other-options"></a>Otras opciones  
 **Editar asignaciones**  
 Use la **asignaciones de columnas** cuadro de diálogo para especificar las columnas de destino para recibir los datos de origen. Puede copiar solo un subconjunto de columnas seleccionando \<omitir > en el **destino** columna de la **asignaciones de columnas** cuadro de diálogo para las columnas que desea omitir.  
  
 **Vista previa**  
 Obtener una vista previa de los datos de origen en el **datos de vista previa** cuadro de diálogo para comprobarlos antes de realizar la importación o exportación. El **datos de vista previa** cuadro de diálogo muestra hasta 200 filas de datos.  
  
 Después de ofrecer una vista previa de los datos, puede que desee cambiar las opciones que ha seleccionado para el origen y el destino. Para realizar estas modificaciones, en la página **Seleccionar tablas y vistas de origen** , haga clic en **Atrás** para volver a las páginas anteriores en las que puede cambiar sus selecciones.  
  
  

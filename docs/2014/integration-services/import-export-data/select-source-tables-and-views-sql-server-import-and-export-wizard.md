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
ms.openlocfilehash: aee638291a4aee2c4ea5d60a69fc206af613e15d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965555"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Seleccionar tablas y vistas de origen (Asistente para importación y exportación de SQL Server)
  Use la página **seleccionar tablas y vistas de origen** para especificar las tablas y vistas que se van a copiar del origen de datos al destino.  
  
> [!NOTE]  
>  No es necesario copiar todas las columnas en una tabla al seleccionar la opción de copia de tabla. Después de seleccionar una tabla de destino, haga clic en Editar asignaciones para mostrar el cuadro de diálogo **asignaciones de columnas** . Seleccione **\<ignore>** en la columna **destino** del cuadro de diálogo **asignaciones de columnas** para las columnas que desea omitir.  
  
 Para obtener más información acerca de este asistente, vea [Asistente para importación y exportación de SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información sobre las opciones para iniciar el asistente y sobre los permisos necesarios para ejecutar el asistente correctamente, vea [ejecutar el Asistente para importación y exportación de SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opciones  
  
### <a name="tables-and-views-list"></a>Lista de tablas y vistas  
 **Origen**  
 Utilice las casillas para seleccionar en la lista las tablas y vistas disponibles que deben copiarse en el destino. Si selecciona una tabla o una vista de origen y no realiza ninguna otra acción, copiará el esquema y los datos del origen sin cambios.  
  
 **Destino**  
 Seleccione una tabla de destino de la lista para cada tabla de origen.  
  
> [!NOTE]  
>  Si interrumpe el asistente en este punto para crear una tabla de destino en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o con otra herramienta, la nueva tabla no será visible de forma inmediata en la lista de tablas de destino disponibles. Para actualizar la lista de tablas de destino, retroceda dos páginas hasta la página **elegir un destino** , vuelva a seleccionar la base de datos de destino y, a continuación, vuelva a avanzar a la **selección de tablas y vistas de origen**.  
  
### <a name="other-options"></a>Otras opciones  
 **Editar asignaciones**  
 Utilice el cuadro de diálogo **asignaciones de columnas** para especificar las columnas de destino que van a recibir los datos de origen. Puede copiar solo un subconjunto de columnas seleccionando \<ignore> en la columna **destino** del cuadro de diálogo **asignaciones de columnas** para las columnas que desea omitir.  
  
 **Versión preliminar**  
 Obtenga una vista previa de los datos de origen en el cuadro de diálogo **vista previa** de los datos para comprobarlo antes de realizar la importación o exportación. El cuadro de diálogo **vista previa** de los datos muestra hasta 200 filas de datos.  
  
 Después de ofrecer una vista previa de los datos, puede que desee cambiar las opciones que ha seleccionado para el origen y el destino. Para realizar estas modificaciones, en la página **Seleccionar tablas y vistas de origen** , haga clic en **Atrás** para volver a las páginas anteriores en las que puede cambiar sus selecciones.  
  
  

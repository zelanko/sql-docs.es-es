---
title: Configurar el destino del archivo plano (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6504e4f5eee83d670b4843fb8d956b23a84d4aad
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58387833"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>Configurar el destino del archivo plano (Asistente para importación y exportación de SQL Server)
  Use la **configurar Flat File Destination** página para especificar opciones de formato para el archivo plano de destino y obtener una vista previa de resultados antes de continuar.  
  
 Para obtener más información acerca de este asistente, vea [Asistente para importación y exportación de SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información acerca de las opciones para iniciar el asistente, así como los permisos necesarios para ejecutar el asistente correctamente, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opciones  
 **Archivo plano de origen**  
 Nombre del archivo de destino.  
  
 **Delimitador de filas**  
 Seleccione los delimitadores de filas de la lista.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**{CR}{LF}**|La fila está delimitada por una combinación de retorno de carro y avance de línea.|  
|**{CR}**|La fila está delimitada por un retorno de carro.|  
|**{LF}**|La fila está delimitada por un avance de línea.|  
|**Punto y coma {;}**|La fila está delimitada por un punto y coma.|  
|**Dos puntos {:}**|La fila está delimitada por dos puntos.|  
|**Coma {,}**|La fila está delimitada por una coma.|  
|**Tabulación {t}**|La fila está delimitada por un tabulador.|  
|**Barra vertical {&#124;}**|La fila está delimitada por una barra vertical.|  
  
 **Delimitador de columna**  
 Seleccione los delimitadores de columna de la lista.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**{CR}{LF}**|Las columnas se delimitan mediante un retorno de carro-combinación de avance de línea.|  
|**{CR}**|Las columnas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las columnas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las columnas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las columnas se delimitan mediante dos puntos.|  
|**Coma {,}**|Las columnas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las columnas se delimitan mediante un tabulador.|  
|**Barra vertical {&#124;}**|Las columnas se delimitan mediante una barra vertical.|  
  
 **Vista previa**  
 Ver en el **datos de vista previa** cuadro de diálogo Opciones de los resultados de la barra de formato seleccionadas para el archivo plano de destino.  
  
 **Editar transformación**  
 Eliminar filas, anexar filas y configurar columnas en el archivo de destino mediante el uso de la **asignaciones de columnas** cuadro de diálogo.  
  
  

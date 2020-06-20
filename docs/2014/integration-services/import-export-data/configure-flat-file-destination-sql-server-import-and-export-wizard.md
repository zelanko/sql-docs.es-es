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
ms.openlocfilehash: 2584cb4a6867d4af3b3f6bc1feff167c900a166d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965618"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>Configurar el destino del archivo plano (Asistente para importación y exportación de SQL Server)
  Use la página **configurar el destino de archivo plano** para especificar las opciones de formato del archivo plano de destino y para obtener una vista previa de los resultados antes de continuar.  
  
 Para obtener más información acerca de este asistente, vea [Asistente para importación y exportación de SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información sobre las opciones para iniciar el asistente, así como los permisos necesarios para ejecutar el asistente correctamente, vea [ejecutar el Asistente para importación y exportación de SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opciones  
 **Archivo plano de origen**  
 Nombre del archivo de destino.  
  
 **Delimitador de filas**  
 Seleccione los delimitadores de filas de la lista.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**{CR}{LF}**|La fila está delimitada por una combinación de retorno de carro y avance de línea.|  
|**COMPRA**|La fila está delimitada por un retorno de carro.|  
|**{LF}**|La fila está delimitada por un avance de línea.|  
|**Punto y coma {;}**|La fila está delimitada por un punto y coma.|  
|**Dos puntos {:}**|La fila está delimitada por dos puntos.|  
|**Unas{,}**|La fila está delimitada por una coma.|  
|**Tabulación {t}**|La fila está delimitada por un tabulador.|  
|**Barra vertical {&#124;}**|La fila está delimitada por una barra vertical.|  
  
 **Delimitador de columna**  
 Seleccione los delimitadores de columna de la lista.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**{CR}{LF}**|Las columnas se delimitan mediante una combinación de retorno de carro y avance de línea.|  
|**COMPRA**|Las columnas se delimitan mediante un retorno de carro.|  
|**{LF}**|Las columnas se delimitan mediante un avance de línea.|  
|**Punto y coma {;}**|Las columnas se delimitan mediante un punto y coma.|  
|**Dos puntos {:}**|Las columnas se delimitan mediante dos puntos.|  
|**Unas{,}**|Las columnas se delimitan mediante una coma.|  
|**Tabulación {t}**|Las columnas se delimitan mediante un tabulador.|  
|**Barra vertical {&#124;}**|Las columnas se delimitan mediante una barra vertical.|  
  
 **Versión preliminar**  
 En el cuadro de diálogo **vista previa** de los datos, los resultados de las opciones de formato seleccionadas para el archivo plano de destino.  
  
 **Editar transformación**  
 Eliminar filas, anexar filas y configurar columnas en el archivo de destino mediante el cuadro de diálogo **asignaciones de columnas** .  
  
  

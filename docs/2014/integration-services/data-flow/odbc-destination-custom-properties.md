---
title: Propiedades personalizadas de los destinos ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 07508c40-6c08-4359-96cd-8ff17671244d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8f9d36b6394aa3921a9262a8b4afc544033c7a20
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62901136"
---
# <a name="odbc-destination-custom-properties"></a>ODBC Destination Custom Properties
  En la tabla siguiente se describen las propiedades personalizadas del destino ODBC. Todas las propiedades se pueden establecer a partir de expresiones SSIS.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|Conexión|Conexión ODBC|Conexión ODBC para acceder a la base de datos de destino.|  
|BatchSize|Entero|Tamaño de lote para la carga masiva. Es el número de filas cargadas como un lote. Esto solo es válido si se admite el enlace de parámetro de modo de fila. Si el enlace parámetro de modo de fila no se admite, el tamaño de lote es 1.|  
|BindCharColumnAs|Integer (enumeración)|Esta propiedad determina cómo el destino ODBC enlaza las columnas con tipos string de varios bytes como SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR.<br /><br /> Los valores posibles son Unicode (0), que enlaza las columnas como SQL_C_WCHAR, y ANSI (1), que enlaza las columnas como SQL_C_CHAR). El valor predeterminado es Unicode (0).<br /><br /> Unicode es la mejor opción para la mayoría de los proveedores ODBC 3.x y los proveedores ODBC 2.x que permiten el enlace de parámetros CHAR como cadenas anchas. Cuando selecciona Unicode y ExposeCharColumnsAsUnicode es True, el usuario no necesita especificar la página de códigos que usa la base de datos de origen.<br /><br /> **Nota:** esta propiedad no está disponible en el **Editor de destino ODBC**, pero se puede establecer con el **Editor avanzado**.|  
|BindNumericAs|Integer (enumeración)|Esta propiedad determina el modo en que el destino ODBC enlaza columnas con datos numéricos con los tipos de datos SQL_TYPE_NUMERIC y SQL_TYPE_DECIMAL.<br /><br /> Los valores posibles son Char (0), que enlaza las columnas como SQL_C_CHAR y Numeric (1), que enlaza las columnas como SQL_C_NUMERIC. El valor predeterminado es Char (0).<br /><br /> **Nota**: esta propiedad no está disponible en el **Editor de destino ODBC**, pero se puede establecer con el **Editor avanzado**.|  
|DefaultCodePage|Entero|Página de códigos que se usará para las columnas de cadena.<br /><br /> **Nota**: esta propiedad no está disponible en el **Editor de destino ODBC**, pero se puede establecer con el **Editor avanzado**.|  
|InsertMethod|Integer (enumeración)|Método usado para insertar los datos. Los valores posibles son fila por fila (0) y lote (1). El valor predeterminado es lote (1).<br /><br /> Para obtener más información sobre estas opciones, vea “Opciones de carga” en [Destino de ODBC](odbc-destination.md).|  
|StatementTimeout|Entero|Número de segundos que se esperará a que una instrucción SQL se ejecute antes de volver, con un error, a la aplicación. El valor predeterminado es 120.|  
|TableName|String|Nombre de la tabla de destino donde los datos se insertan.|  
|TransactionSize|Entero|Número de inserciones en una sola transacción. El valor predeterminado es 0, que significa que el destino ODBC funciona en modo de confirmación automática.<br /><br /> Dado que el administrador de conexiones ODBC no admite transacciones distribuidas, es posible establecer esta propiedad con un valor distinto de 0. Sin embargo, si la propiedad **RetainSameConnection** del administrador de conexiones se establece en **true** , esta propiedad se debe establecer en 0.<br /><br /> **Nota**: esta propiedad no está disponible en el **Editor de destino ODBC**, pero se puede establecer con el **Editor avanzado**.|  
|LobChunkSize|Entero|Asignación de tamaño del fragmento para las columnas LOB.|  
  
  

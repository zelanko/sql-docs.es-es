---
title: "Sección SQL del archivo de personalización | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e0cb92bcd2ea9580fa8824a50b15a1f60cdf35c3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="customization-file-sql-section"></a>Sección SQL del archivo de personalización
El **sql** sección puede contener una nueva cadena SQL que reemplaza la cadena de comandos de cliente. Si no hay ninguna cadena de SQL en la sección, se omitirá la sección.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 La nueva cadena SQL puede ser *con parámetros*. Es decir, los parámetros en la **sql** sección cadena SQL (designado por el '?' caracteres) pueden ser reemplazados por los argumentos correspondientes de un *identificador* en la cadena de comandos de cliente (designado por un lista separados con comas entre paréntesis). El identificador y la lista de argumentos se comportan como una llamada de función.  
  
 Por ejemplo, suponga que la cadena de comandos de cliente es `"CustomerByID(4)"`, el encabezado de sección SQL es `[SQL CustomerByID]`, y la nueva cadena de la sección SQL es `"SELECT * FROM Customers WHERE CustomerID = ?".` el controlador generará `"SELECT * FROM Customers WHERE CustomerID = 4"` y utilizará dicha cadena para consultar el origen de datos.  
  
 Si la nueva instrucción SQL es la cadena null (""), a continuación, se omite la sección.  
  
 Si la nueva cadena de la instrucción SQL no es válida, se producirá un error en la ejecución de la instrucción. Se omite el parámetro de cliente. Puede hacerlo intencionadamente para "desactivar" todos los comandos SQL de cliente especificando:  
  
```  
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>Sintaxis  
 Un entrada de cadena SQL de reemplazo tiene el formato:  
  
 **SQL =**   
 ***sqlString***  
  
|Parte|Description|  
|----------|-----------------|  
|**SQL**|Una cadena literal que indica que esta es una entrada de la sección SQL.|  
|***sqlString***|Una cadena SQL que reemplaza la cadena de cliente.|  
  
## <a name="see-also"></a>Vea también  
 [Sección Connect del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección UserList del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Opciones de cliente necesarias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción de los archivos de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



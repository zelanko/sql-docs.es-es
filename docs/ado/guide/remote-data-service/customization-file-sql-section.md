---
title: Sección SQL del archivo de personalización | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36f6eec4b8203848dc6f4b8c99597f22c9cedeab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47625883"
---
# <a name="customization-file-sql-section"></a>Sección de SQL del archivo de personalización
El **sql** sección puede contener una cadena SQL nueva que reemplaza la cadena de comandos de cliente. Si no hay ninguna cadena SQL en la sección, se omitirá la sección.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Puede ser la nueva cadena SQL *parametrizada*. Es decir, los parámetros en el **sql** cadena SQL de la sección (designado por el '?' caracteres) puede reemplazarse con los argumentos correspondientes en un *identificador* en la cadena de comandos de cliente (designado por un lista separados con comas entre paréntesis). El identificador y la lista de argumentos se comportan como una llamada de función.  
  
 Por ejemplo, suponga que la cadena de comandos de cliente es `"CustomerByID(4)"`, el encabezado de la sección SQL es `[SQL CustomerByID]`, y es la nueva cadena de la sección SQL `"SELECT * FROM Customers WHERE CustomerID = ?".` el controlador generará `"SELECT * FROM Customers WHERE CustomerID = 4"` y usar esa cadena para consultar el origen de datos.  
  
 Si la nueva instrucción SQL es la cadena nula (""), a continuación, se omite la sección.  
  
 Si la nueva cadena de instrucción SQL no es válida, se producirá un error en la ejecución de la instrucción. Se omite el parámetro del cliente. Puede hacerlo intencionadamente para "desactivar" todos los comandos SQL de cliente especificando:  
  
```  
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>Sintaxis  
 Un entrada de la cadena SQL de reemplazo tiene el formato:  
  
 **SQL =**   
 ***SqlString***  
  
|Parte|Descripción|  
|----------|-----------------|  
|**SQL**|Una cadena literal que indica que esta es una entrada de la sección SQL.|  
|***SqlString***|Una cadena SQL que reemplaza la cadena de cliente.|  
  
## <a name="see-also"></a>Vea también  
 [Sección de conexión del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección UserList del archivo personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configuración de cliente requerida](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción del archivo de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



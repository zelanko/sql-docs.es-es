---
title: Sección SQL del archivo de personalización | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: e65c2871-9986-44ff-b8b7-7f5eda91b3fa
author: rothja
ms.author: jroth
ms.openlocfilehash: 934b982004bf27e28a8daeed09061101886ce444
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82749876"
---
# <a name="customization-file-sql-section"></a>Sección de SQL del archivo de personalización
La sección **SQL** puede contener una nueva cadena de SQL que reemplaza la cadena de comando del cliente. Si no hay ninguna cadena de SQL en la sección, se omitirá la sección.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 La nueva cadena SQL se puede *parametrizar*. Es decir, los parámetros de la sección **SQL** cadena SQL (designada por el carácter '? ') se pueden reemplazar por los argumentos correspondientes en un *identificador* en la cadena de comandos del cliente (designada por una lista delimitada por comas entre paréntesis). El identificador y la lista de argumentos se comportan como una llamada de función.  
  
 Por ejemplo, supongamos que la cadena de comandos del cliente es `"CustomerByID(4)"` , el encabezado de la sección SQL es `[SQL CustomerByID]` y la nueva cadena de la sección SQL es `"SELECT * FROM Customers WHERE CustomerID = ?".` el controlador que generará `"SELECT * FROM Customers WHERE CustomerID = 4"` y usará esa cadena para consultar el origen de datos.  
  
 Si la nueva instrucción SQL es la cadena null (""), se omite la sección.  
  
 Si la nueva cadena de instrucción SQL no es válida, se producirá un error en la ejecución de la instrucción. El parámetro Client se omite en efecto. Puede hacer esto intencionadamente para "desactivar" todos los comandos SQL de cliente especificando:  
  
```console
[SQL default]   
SQL = " "  
```  
  
## <a name="syntax"></a>Sintaxis  
 Una entrada de cadena SQL de reemplazo tiene el formato:  
  
 **SQL =**   
 ***sqlString***  
  
|Parte|Descripción|  
|----------|-----------------|  
|**SQL**|Cadena literal que indica que se trata de una entrada de sección SQL.|  
|***sqlString***|Cadena de SQL que reemplaza la cadena de cliente.|  
  
## <a name="see-also"></a>Consulte también  
 [Sección de conexión del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección de registros de archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección UserList del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configuración de cliente requerida](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción del archivo de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



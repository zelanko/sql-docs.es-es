---
title: Configuración de cliente requerida | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb864cb5489cc5cd1a82343995ed7a1e73c3a0b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="required-client-settings"></a>Opciones de cliente necesarias
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Especifique la siguiente configuración para utilizar un personalizado **DataFactory** controlador.  
  
-   Especifique "proveedor = MS Remote" en la [conexión ADO (objetos)](../../../ado/reference/ado-api/connection-object-ado.md) objeto [propiedad de proveedor (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) propiedad o el **conexión** objeto de cadena de conexión "**Proveedor**= "palabra clave.  
  
-   Establecer el [propiedad CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient**.  
  
-   Especifique el nombre del controlador que se va a usar en el [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) del objeto **controlador** propiedad, o la [conjunto de registros ADO (objetos)](../../../ado/reference/ado-api/recordset-object-ado.md) "delacadenadeconexióndeobjeto **Controlador**= "palabra clave. (No se puede establecer el controlador el **conexión** cadena de conexión del objeto.)  
  
 RDS proporciona un controlador predeterminado en el servidor denominado **MSDFMAP. Controlador**. (El archivo de personalización predeterminado se denomina MSDFMAP. INI).  
  
 **Ejemplo**  
  
 Se supone que las siguientes secciones **MSDFMAP. INI** y el nombre del origen de datos AdvWorks, se han definido previamente:  
  
```  
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 Los fragmentos de código siguiente se escriben en Visual Basic:  
  
## <a name="rdsdatacontrol-version"></a>RDS. Versión de DataControl  
  
```  
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "http://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>Versión del conjunto de registros  
  
```  
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 Especifique el [propiedad de controlador (RDS)](../../../ado/reference/rds-api/handler-property-rds.md) propiedad o palabra clave; el [propiedad de proveedor (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) propiedad o palabra clave; y la *CustomerById* y  *CustomerDatabase* identificadores. A continuación, abra el **Recordset** objeto  
  
 RS. Abra "CustomerById (4)", "controlador = MSDFMAP. Controlador;"& _  
  
```  
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=http://yourServer"  
```  
  
## <a name="see-also"></a>Vea también  
 [Sección Connect del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sección UserList del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Opciones de cliente necesarias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción de los archivos de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)























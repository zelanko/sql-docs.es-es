---
title: Configuración de cliente requerida | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bdb99cb3d792900f48ceb69c25c7ae720c339683
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922292"
---
# <a name="required-client-settings"></a>Configuración de cliente requerida
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Especifique la siguiente configuración para utilizar una personalizada **DataFactory** controlador.  
  
-   Especifique "proveedor = MS Remote" en la [conexión ADO (objetos)](../../../ado/reference/ado-api/connection-object-ado.md) objeto [propiedad de proveedor (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) propiedad o el **conexión** objeto de cadena de conexión "**Proveedor**= "palabra clave.  
  
-   Establecer el [propiedad CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient**.  
  
-   Especifique el nombre del controlador para usar en el [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) del objeto **controlador** propiedad, o la [conjunto de registros ADO (objetos)](../../../ado/reference/ado-api/recordset-object-ado.md) "delacadenadeconexióndeobjeto **Controlador**= "palabra clave. (El controlador no se puede establecer en el **conexión** cadena de conexión del objeto.)  
  
 RDS proporciona un controlador predeterminado en el servidor denominado **MSDFMAP. Controlador**. (El archivo de personalización predeterminado se denomina MSDFMAP. INI.)  
  
 **Ejemplo**  
  
 Se supone que las siguientes secciones **MSDFMAP. INI** y el nombre del origen de datos AdvWorks, se han definido previamente:  
  
```console
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 Los siguientes fragmentos de código están escritos en Visual Basic:  
  
## <a name="rdsdatacontrol-version"></a>RDS. Versión de control de datos  
  
```vb
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "https://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>Versión del conjunto de registros  
  
```vb
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 Especifique el [propiedad de controlador (RDS)](../../../ado/reference/rds-api/handler-property-rds.md) propiedad o la palabra clave; el [propiedad de proveedor (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) propiedad o la palabra clave; y la *CustomerById* y  *CustomerDatabase* identificadores. A continuación, abra el **Recordset** objeto  
  
 RS. Abra "CustomerById (4)", "controlador = MSDFMAP. Controlador;"& _  
  
```vb
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=https://yourServer"  
```  
  
## <a name="see-also"></a>Vea también  
 [Sección de conexión del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sección UserList del archivo personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configuración de cliente requerida](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción del archivo de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


---
title: Escribir un controlador personalizado | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 58a380336d3b1abc99e00f1f4052cd24a8cc5988
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699404"
---
# <a name="writing-your-own-customized-handler"></a>Escritura de un controlador personalizado
Es posible que desea escribir su propio controlador si es un administrador del servidor IIS que desea que el valor predeterminado admite RDS, pero un mayor control sobre las solicitudes de usuario y los derechos de acceso.  
  
 MSDFMAP. Controlador implementa el **IDataFactoryHandler** interfaz.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="idatafactoryhandler-interface"></a>Interfaz IDataFactoryHandler  
 Esta interfaz tiene dos métodos, **GetRecordset** y **volver a conectar**. Ambos métodos requieren que el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad se establece en **adUseClient**.  
  
 Ambos métodos toman argumentos que aparecen después de la primera coma en el "**controlador =** " palabra clave. Por ejemplo, `"Handler=progid,arg1,arg2;"` pasará una cadena de argumentos `"arg1,arg2"`, y `"Handler=progid"` pasará un argumento nulo.  
  
## <a name="getrecordset-method"></a>Método GetRecordset  
 Este método consulta el origen de datos y crea un nuevo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto con los argumentos proporcionados. El **Recordset** debe abrirse con **adLockBatchOptimistic** y no se debe abrir de forma asincrónica.  
  
### <a name="arguments"></a>Argumentos  
 ***conn*** la cadena de conexión.  
  
 ***args*** los argumentos para el controlador.  
  
 ***consulta*** el texto del comando para realizar una consulta.  
  
 ***ppRS:*** el puntero donde el **Recordset** se deben devolver.  
  
## <a name="reconnect-method"></a>Volver a conectar (método)  
 Este método actualiza el origen de datos. Crea un nuevo [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto y se conecta el determinado **Recordset**.  
  
### <a name="arguments"></a>Argumentos  
 ***conn*** la cadena de conexión.  
  
 ***args*** los argumentos para el controlador.  
  
 ***incorporación de cambios*** A **Recordset** objeto.  
  
## <a name="msdfhdlidl"></a>msdfhdl.idl  
 Se trata de la definición de interfaz **IDataFactoryHandler** que aparece en el **msdfhdl.idl** archivo.  
  
```cpp
[  
  uuid(D80DE8B3-0001-11d1-91E6-00C04FBBBFB3),  
  version(1.0)  
]  
library MSDFHDL  
{  
    importlib("stdole32.tlb");  
    importlib("stdole2.tlb");  
  
    // TLib : Microsoft ActiveX Data Objects 2.0 Library  
    // {00000200-0000-0010-8000-00AA006D2EA4}  
    #ifdef IMPLIB  
    importlib("implib\\x86\\release\\ado\\msado15.dll");  
    #else  
    importlib("msado20.dll");  
    #endif  
  
    [  
      odl,  
      uuid(D80DE8B5-0001-11d1-91E6-00C04FBBBFB3),  
      version(1.0)  
    ]  
    interface IDataFactoryHandler : IUnknown  
    {  
HRESULT _stdcall GetRecordset(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] BSTR query,  
      [out, retval] _Recordset **ppRS);  
  
// DataFactory will use the ActiveConnection property  
// on the Recordset after calling Reconnect.  
   HRESULT _stdcall Reconnect(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] _Recordset *pRS);  
    };  
};  
```  
  
## <a name="see-also"></a>Vea también  
 [Sección de conexión del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sección UserList del archivo personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configuración de cliente requerida](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción del archivo de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)



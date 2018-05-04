---
title: Escribir su propio controlador personalizado | Documentos de Microsoft
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
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b780e2027e64f7832fd622e66e1d908696d24b0e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="writing-your-own-customized-handler"></a>Escribir su propio controlador personalizado
Puede que desee escribir su propio controlador si es un administrador del servidor IIS que desea que el valor predeterminado RDS admite, pero tener más control sobre las solicitudes de usuario y los derechos de acceso.  
  
 MSDFMAP. Controlador implementa la **IDataFactoryHandler** interfaz.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="idatafactoryhandler-interface"></a>Interfaz IDataFactoryHandler  
 Esta interfaz tiene dos métodos, **GetRecordset** y **volver a conectar**. Ambos métodos requieren que el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad se establece en **adUseClient**.  
  
 Ambos métodos toman argumentos que aparecen detrás de la primera coma en la "**controlador =**" (palabra clave). Por ejemplo, `"Handler=progid,arg1,arg2;"` pasará una cadena de argumentos `"arg1,arg2"`, y `"Handler=progid"` pasará un argumento nulo.  
  
## <a name="getrecordset-method"></a>Método GetRecordset  
 Este método consulta el origen de datos y crea un nuevo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto con los argumentos proporcionados. El **Recordset** debe abrirse con **adLockBatchOptimistic** y no se debe abrir de forma asincrónica.  
  
### <a name="arguments"></a>Argumentos  
 ***conn*** la cadena de conexión.  
  
 ***args*** los argumentos para el controlador.  
  
 ***consulta*** el texto del comando para realizar una consulta.  
  
 ***ppRS:*** el puntero donde la **Recordset** se deben devolver.  
  
## <a name="reconnect-method"></a>Volver a conectar (método)  
 Este método actualiza el origen de datos. Crea un nuevo [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto y adjuntará el determinado **conjunto de registros**.  
  
### <a name="arguments"></a>Argumentos  
 ***conn*** la cadena de conexión.  
  
 ***args*** los argumentos para el controlador.  
  
 ***Pr*** A **Recordset** objeto.  
  
## <a name="msdfhdlidl"></a>msdfhdl.idl  
 Se trata de la definición de interfaz para **IDataFactoryHandler** que aparece en el **msdfhdl.idl** archivo.  
  
```  
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
 [Sección Connect del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sección UserList del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Opciones de cliente necesarias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción del archivo de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)



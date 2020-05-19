---
title: Escribir su propio controlador personalizado | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: cd7aec0e98afd09b30c4e4d67102d1333efdcdd6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747603"
---
# <a name="writing-your-own-customized-handler"></a>Escritura de un controlador personalizado
Es posible que desee escribir su propio controlador si es un administrador del servidor IIS que desea la compatibilidad predeterminada de RDS, pero más control sobre las solicitudes de usuario y los derechos de acceso.  
  
 El MSDFMAP. El controlador implementa la interfaz **IDataFactoryHandler** .  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="idatafactoryhandler-interface"></a>Interfaz IDataFactoryHandler  
 Esta interfaz tiene dos métodos, **GetRecordset** y **reconnect**. Ambos métodos requieren que la propiedad [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) esté establecida en **adUseClient**.  
  
 Ambos métodos toman los argumentos que aparecen después de la primera coma en la palabra clave "**handler =**". Por ejemplo, pasará `"Handler=progid,arg1,arg2;"` una cadena de argumento de `"arg1,arg2"` y pasará `"Handler=progid"` un argumento null.  
  
## <a name="getrecordset-method"></a>GetRecordset (método)  
 Este método consulta el origen de datos y crea un nuevo objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) con los argumentos proporcionados. El **conjunto de registros** debe abrirse con **adLockBatchOptimistic** y no debe abrirse de forma asincrónica.  
  
### <a name="arguments"></a>Argumentos  
 ***Conn***  Cadena de conexión.  
  
 ***argumentos***  Argumentos para el controlador.  
  
 ***consulta*** de  Texto del comando para realizar una consulta.  
  
 ***ppRS***  Puntero en el que se debe devolver el **conjunto de registros** .  
  
## <a name="reconnect-method"></a>Reconnect (método)  
 Este método actualiza el origen de datos. Crea un nuevo objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) y adjunta el conjunto de **registros**especificado.  
  
### <a name="arguments"></a>Argumentos  
 ***Conn***  Cadena de conexión.  
  
 ***argumentos***  Argumentos para el controlador.  
  
 ***PR***  Objeto de **conjunto de registros** .  
  
## <a name="msdfhdlidl"></a>msdfhdl. idl  
 Se trata de la definición de interfaz para **IDataFactoryHandler** que aparece en el archivo **msdfhdl. idl** .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Sección de conexión del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Sección de registros de archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Sección SQL de archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Sección UserList del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configuración de cliente requerida](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Descripción del archivo de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)



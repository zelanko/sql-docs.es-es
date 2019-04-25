---
title: Páginas de códigos de servidor y los datos Unicode | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- metadata [SQL Server], stored procedures
- Unicode [SQL Server], extended stored procedures
- extended stored procedures [SQL Server], metadata
ms.assetid: 52310260-a892-4b27-ad2e-bf164b98ee80
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b7c992f8b33e2eb96b0e6ea7eec1f58beaf8aefd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62511830"
---
# <a name="unicode-data-and-server-code-pages"></a>Datos Unicode y páginas de códigos de servidor
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 La API Procedimiento almacenado extendido está habilitada para los datos Unicode; sin embargo, no está habilitada para los metadatos Unicode. La directiva #define de Unicode no tiene ningún efecto en la API Procedimiento almacenado extendido.  
  
 Se supone que todos los metadatos que devuelve la API Procedimiento almacenado extendido o que la aplicación de procedimiento almacenado extendida le proporciona están en la página de códigos multibyte del servidor. La página de códigos predeterminada de una aplicación de servidor de API procedimiento almacenado extendido es la página de códigos ANSI del equipo donde se ejecuta la aplicación, que puede obtenerse mediante una llamada a **srv_pfield** con el parámetro de campo establecido en SRV_ SPROC_CODEPAGE.  
  
 Si la aplicación de API Procedimiento almacenado extendido está habilitada para Unicode, debe convertir los nombres de columna de metadatos de Unicode, mensajes de error, etc., a datos multibyte antes de pasar estos datos a la API Procedimiento almacenado extendido.  
  
## <a name="example"></a>Ejemplo  
 El siguiente procedimiento almacenado extendido proporciona un ejemplo de las conversiones de Unicode tratadas. Tenga en cuenta lo siguiente:  
  
-   Datos de columna se pasan como datos Unicode a **srv_describe** porque la columna se describe como srvnvarchar.  
  
-   Metadatos de nombre de columna se pasan a **srv_describe** como datos multibyte.  
  
     Las llamadas a procedimiento almacenado extendido **srv_pfield** con el parámetro de campo establecido en SRV_SPROC_CODEPAGE para obtener la página de códigos multibyte [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Los mensajes de error que se pasan a **srv_sendmsg** como datos multibyte.  
  
    ```  
    __declspec(dllexport) RETCODE proc1 (SRV_PROC *srvproc)  
    {  
        #define MAX_COL_NAME_LEN 25  
        #define MAX_COL_DATA_LEN 50  
        #define MAX_ERR_MSG_LEN 250  
        #define MAX_SERVER_ERROR 20000  
        #define XP_ERROR_NUMBER MAX_SERVER_ERROR+1  
  
        int retval;  
        UINT serverCodePage;  
        CHAR *szServerCodePage;  
  
        WCHAR unicodeColumnName[MAX_COL_NAME_LEN];  
        CHAR multibyteColumnName[MAX_COL_NAME_LEN];  
  
        WCHAR unicodeColumnData[MAX_COL_DATA_LEN];  
  
        WCHAR unicodeErrorMessage[MAX_ERR_MSG_LEN];  
        CHAR  multibyteErrorMessage[MAX_ERR_MSG_LEN];  
  
        lstrcpyW (unicodeColumnName, L"column1");  
        lstrcpyW (unicodeColumnData, L"column1 data");  
        lstrcpyW (unicodeErrorMessage, L"No Error!");  
  
        // Obtain server code page.  
        //  
        szServerCodePage = srv_pfield (srvproc, SRV_SPROC_CODEPAGE, NULL);      
        if (NULL != szServerCodePage)  
            serverCodePage = atol(szServerCodePage);  
        else   
        {   // Problem situation exists.  
            srv_senddone(srvproc, (SRV_DONE_ERROR | SRV_DONE_MORE), 0, 0);  
            return 1;  
        }  
  
        // Convert column name for Unicode to multibyte using the   
        // server code page.  
        //  
        retval = WideCharToMultiByte(    
            serverCodePage,                 // code page  
            0,                              // default  
            unicodeColumnName,              // wide-character string  
            -1,                             // string is null terminated  
            multibyteColumnName,            // address of buffer for new  
                                            //   string  
            sizeof (multibyteColumnName),   // size of buffer  
            NULL, NULL);  
  
        if (0 == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"Conversion to multibyte  
            failed.");  
            goto Error;  
        }  
  
        retval = srv_describe (srvproc, 1, multibyteColumnName,  
        SRV_NULLTERM,   
          SRVNVARCHAR, MAX_COL_DATA_LEN*sizeof(WCHAR), // destination  
            SRVNVARCHAR, lstrlenW(unicodeColumnData)*sizeof(WCHAR),  
            unicodeColumnData); //source  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_describe failed.");  
            goto Error;  
        }  
  
       retval = srv_sendrow(srvproc);  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_sendrow failed.");  
            goto Error;  
        }  
  
        retval = srv_senddone (srvproc, SRV_DONE_MORE|SRV_DONE_COUNT, 0, 1);  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_senddone failed.");  
            goto Error;  
        }  
  
        return 0;  
    Error:  
        // convert error message from Unicode to multibyte.  
        retval = WideCharToMultiByte(    
            serverCodePage,                 // code page  
            0,                              // default  
            unicodeErrorMessage,            // wide-character string  
            -1,                             // string is null terminated  
            multibyteErrorMessage,          // address of buffer for new  
                                            //   string  
            sizeof (multibyteErrorMessage), // size of buffer  
            NULL, NULL);  
  
    srv_sendmsg(srvproc, SRV_MSG_ERROR, XP_ERROR_NUMBER, SRV_INFO, 1,  
                NULL, 0, __LINE__,   
                multibyteErrorMessage,  
                SRV_NULLTERM);  
  
        srv_senddone(srvproc, (SRV_DONE_ERROR | SRV_DONE_MORE), 0, 0);  
  
        return 1;  
    }  
  
    ```  
  
## <a name="see-also"></a>Vea también  
 [srv_wsendmsg &#40;API procedimiento almacenado extendido&#41;](../extended-stored-procedures-reference/srv-wsendmsg-extended-stored-procedure-api.md)  
  
  

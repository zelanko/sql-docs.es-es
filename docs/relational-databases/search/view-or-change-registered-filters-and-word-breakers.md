---
title: Ver o cambiar los filtros y separadores de palabras registrados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], word breakers
- full-text search [SQL Server], filters
- filters [full-text search]
- word breakers [full-text search]
ms.assetid: f88c54df-b1aa-4701-807f-dc92c32363fd
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 278100271fafdafa631d981bc43cc2460706df71
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="view-or-change-registered-filters-and-word-breakers"></a>Ver o cambiar los filtros y separadores de palabras registrados
  Después de instalar o desinstalar filtros o separadores de palabras en un sistema, los cambios no se aplican automáticamente en las instancias de servidor. En este tema se describe cómo ver los filtros o separadores de palabras actualmente registrados y cómo registrar filtros y separadores de palabras recién instalados en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="to-view-a-list-of-languages-whose-word-breakers-are-currently-registered"></a>Para ver una lista de idiomas con separadores de palabras actualmente registrados  
  
1.  Use la vista de catálogo [sys.fulltext_languages](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) , tal y como se muestra a continuación:  
  
    ```  
    SELECT * FROM sys.fulltext_languages;   
    ```  
  
### <a name="to-view-a-list-of-the-filters-that-are-currently-registered"></a>Para ver una lista de los filtros actualmente registrados  
  
1.  Use el procedimiento almacenado del sistema [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) , tal y como se muestra a continuación:  
  
    ```  
    EXEC sp_help_fulltext_system_components 'filter';    
    ```  
  
### <a name="to-register-newly-installed-word-breakers-and-filters"></a>Para registrar filtros y separadores de palabras recién instalados  
  
1.  Use el procedimiento almacenado del sistema [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md) para actualizar la lista de idiomas, tal y como se muestra a continuación:  
  
    ```  
    exec sp_fulltext_service 'update_languages';   
    ```  
  
### <a name="to-unregister-uninstalled-word-breakers-and-filters"></a>Para anular el registro de filtros y separadores de palabras instalados  
  
1.  Use **sp_fulltext_service** para actualizar la lista de idiomas, tal y como se muestra a continuación:  
  
    ```  
    exec sp_fulltext_service 'update_languages'  
    ```  
  
2.  Use **sp_fulltext_service** para reiniciar los procesos de host de demonio de filtro (fdhost.exe), tal y como se muestra a continuación:  
  
    ```  
    exec sp_fulltext_service 'restart_all_fdhosts';  
    ```  
  
### <a name="to-replace-existing-word-breakers-or-filters-when-installing-new-ones"></a>Para reemplazar los filtros o separadores de palabras existentes al instalar filtros o separadores de palabras nuevos  
  
1.  Cuando se prepare para instalar un archivo DLL que contenga nuevos filtros o separadores de palabras, compruebe que tenga un nombre de archivo distinto de cualquiera de los archivos DLL existentes instalados en su instancia del servidor.  
  
2.  Copie el nuevo archivo DLL en el directorio que contiene los archivos DLL estándar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la instancia del servidor. La ubicación predeterminada es:  
  
     C:\Archivos de programa\Microsoft SQL Server\MSSQL.*nombre_instancia*\MSSQL\Binn  
  
    > [!IMPORTANT]  
    >  Se recomienda encarecidamente que solamente cargue componentes firmados y comprobados. También se recomienda que ejecute el servicio del iniciador de FDHOST (MSSQLFDLauncher) con la menor cantidad de privilegios posible.  
  
3.  Instale los nuevos filtros o separadores de palabras.  
  
     **Para instalar y cargar IFilters de Microsoft Filter Pack**  
  
    -   [Cómo registrar IFilters de Microsoft Filter Pack con SQL Server](http://go.microsoft.com/fwlink/?LinkId=130439)  
  
4.  Use **sp_fulltext_service** para cargar los filtros y separadores de palabras recién instalados en la instancia del servidor, tal y como se muestra a continuación:  
  
    ```  
    EXEC sp_fulltext_service @action='load_os_resources', @value=1;  
    ```  
  
5.  Use **sp_fulltext_service** para actualizar la lista de idiomas, tal y como se muestra a continuación:  
  
    ```  
    EXEC sp_fulltext_service 'update_languages';  
    ```  
  
6.  Reinicie los procesos de host de demonio de filtro (fdhost.exe) mediante **sp_fulltext_service** , tal y como se muestra a continuación:  
  
    ```  
    EXEC sp_fulltext_service 'restart_all_fdhosts';   
    ```  
  
## <a name="see-also"></a>Vea también  
 [Establecer la cuenta del servicio para el selector del demonio de filtro completo](../../relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [Configurar y administrar filtros para búsquedas](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [Configurar y administrar separadores de palabras y lematizadores para la búsqueda](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  

---
title: Configurar o cambiar la intercalación del servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- server collations [SQL Server]
- collations [SQL Server], server
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4501bc77a28746de3b0ce97b7b619889093650d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62918582"
---
# <a name="set-or-change-the-server-collation"></a>Configurar o cambiar la intercalación del servidor
  La intercalación de servidor actúa como intercalación predeterminada para todas las bases de datos del sistema que se han instalado con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como las bases de datos de usuario recién creadas. La intercalación de servidor se especifica durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para más información, consulte [Compatibilidad con la intercalación y Unicode](collation-and-unicode-support.md).  
  
## <a name="changing-the-server-collation"></a>Cambiar la intercalación de servidor  
 El cambio de la intercalación predeterminada para una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ser una operación compleja que incluye los siguientes pasos:  
  
-   Asegurarse de que se dispone de toda la información o scripts necesarios para volver a crear las bases de datos de usuario y todos los objetos contenidos en ellas.  
  
-   Exportar todos los datos mediante una herramienta como [bcp Utility](../../tools/bcp-utility.md). Para obtener más información, vea [Importar y exportar datos en bloque &#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md).  
  
-   Quitar todas las bases de datos de usuario.  
  
-   Vuelva a generar la base de datos maestra al especificar la nueva intercalación en la propiedad SQLCOLLATION del comando **setup** . Por ejemplo:  
  
    ```  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName   
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]   
    /SQLCOLLATION=CollationName  
    ```  
  
     Para obtener más información, vea [Volver a generar bases de datos del sistema](../databases/system-databases.md).  
  
-   Crear todas las bases de datos y todos los objetos contenidos en ellas.  
  
-   Importar todos los datos.  
  
> [!NOTE]  
>  En lugar de cambiar la intercalación predeterminada de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede especificar una intercalación predeterminada para cada nueva base de datos que cree.  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad con la intercalación y Unicode](collation-and-unicode-support.md)   
 [Establecer o cambiar la intercalación de base de datos](set-or-change-the-database-collation.md)   
 [Establecer o cambiar la intercalación de columnas](set-or-change-the-column-collation.md)   
 [Volver a generar bases de datos del sistema](../databases/system-databases.md)  
  
  

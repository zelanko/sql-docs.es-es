---
title: 'Lección 2: Preparación de la carpeta de instantáneas | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f286cde9-c0d0-43ef-b7ba-53c3cbb8906c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bbe571002a1168ca3f60592b86fb58fd482ecd05
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000429"
---
# <a name="lesson-2-preparing-the-snapshot-folder"></a>Lección 2: Preparar la carpeta de instantáneas
  En esta lección aprenderá a configurar la carpeta de instantáneas que se utiliza para crear y almacenar la instantánea de publicación.  
  
### <a name="to-create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>Para crear un recurso compartido para la carpeta de instantáneas y asignar permisos  
  
1.  En el Explorador de Windows, navegue a la carpeta de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La ubicación predeterminada es C:\Archivos de programa\Microsoft SQL Server\MSSQL.X\MSSQL\Data.  
  
2.  Cree una carpeta con el nombre **repldata**.  
  
3.  Haga clic con el botón derecho en esta carpeta y haga clic en **Propiedades**.  
  
4.  En la pestaña **Compartir** del cuadro de diálogo **Propiedades de repldata** , haga clic en **Compartir**.  
  
5.  En el cuadro de diálogo **Uso compartido de archivos** , haga clic en **Compartir**y luego en **Listo**.  
  
6.  En la pestaña **Seguridad** , haga clic en **Editar**.  
  
7.  En el cuadro de diálogo **Permisos** , haga clic en **Agregar**. En el cuadro de texto **Seleccionar usuarios, equipos, cuentas de servicio o grupos** , escriba el nombre de la cuenta de agente de instantáneas creada en la lección 1, como \< _Machine_Name>_ **\ repl_snapshot**, donde \< *Machine_Name>* es el nombre del publicador. Haga clic en **Comprobar nombres**y luego en **Aceptar**.  
  
8.  Repita el paso anterior para agregar permisos para el Agente de distribución, como \< _Machine_Name>_ **\ repl_distribution**y para el Agente de mezcla como \< _Machine_Name _>**\ repl_merge**.  
  
9. Compruebe que se admiten los siguientes permisos:  
  
    -   repl_snapshot - Control total  
  
    -   repl_distribution - Lectura  
  
    -   repl_merge - Lectura  
  
10. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades de repldata** y crear el recurso compartido repldata.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha configurado correctamente el recurso compartido para la carpeta de instantáneas. A continuación configurará la distribución. Consulte [Lección 3: Configurar la distribución](lesson-3-configuring-distribution.md).  
  
## <a name="see-also"></a>Consulte también  
 [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md)  
  
  

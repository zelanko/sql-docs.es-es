---
title: Establecer un tamaño máximo de archivo para un archivo de seguimiento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- maximum file size for traces
- size [SQL Server], trace files
ms.assetid: e86dc4ce-5aa3-4c0d-acb5-c9e8871ed963
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e0bb761cf3402080842ae0eaff7b04a0f312a3a4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52775237"
---
# <a name="set-a-maximum-file-size-for-a-trace-file-sql-server-profiler"></a>Establecer un tamaño máximo de archivo para un archivo de seguimiento (SQL Server Profiler)
  Utilice el siguiente procedimiento para establecer el tamaño máximo de archivo para un archivo de seguimiento.  
  
### <a name="to-set-a-maximum-file-size-for-a-trace-file"></a>Para establecer un tamaño máximo de archivo para un archivo de seguimiento  
  
1.  En el menú **Archivo** , haga clic en **Nueva seguimiento**y conéctese a una instancia de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Aparecerá el cuadro de diálogo **Propiedades de seguimiento**.  
  
    > [!NOTE]  
    >  Si se selecciona **Iniciar el seguimiento inmediatamente tras realizar la conexión**, el cuadro de diálogo **Propiedades de seguimiento**no aparecerá y, en su lugar, se iniciará el seguimiento. Para desactivar esta configuración, en el menú **Herramientas**, haga clic en **Opciones**y desactive la casilla **Iniciar el seguimiento inmediatamente tras realizar la conexión** .  
  
2.  En el cuadro **Nombre de seguimiento** , escriba un nombre para el seguimiento.  
  
3.  En el cuadro **Nombre de plantilla**, seleccione una plantilla de seguimiento.  
  
4.  Seleccione **Guardar en el archivo**y, a continuación, especifique un archivo en el que almacenar la información del seguimiento.  
  
5.  En la casilla **Establecer el tamaño máximo de archivo (MB)** , especifique un tamaño máximo de archivo para el seguimiento. Cuando el archivo alcanza este tamaño máximo, se dejan de registrar eventos de seguimiento en el archivo. Si selecciona **Habilitar sustitución incremental de archivos** (seleccionada de manera predeterminada), ocurre lo siguiente:  
  
     La opción de sustitución incremental de archivos hace que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cierre el archivo actual y cree un archivo nuevo al alcanzar el tamaño máximo de archivo. El nuevo archivo tiene el mismo nombre que el archivo anterior, pero se le anexa un número entero al nombre para indicar la secuencia; por ejemplo, si el archivo de seguimiento original se denomina filename_1.trc, el siguiente archivo de seguimiento es filename_2.trc, etc. Si un archivo existente ya utiliza el nombre asignado a un archivo nuevo de sustitución incremental, el archivo existente se sobrescribe, a menos que sea de solo lectura. Esta opción de sustitución incremental de archivos está habilitada de forma predeterminada cuando guarda datos de un seguimiento en un archivo.  
  
     Con la opción de sustitución incremental de archivos activada, el seguimiento continúa hasta que se detiene por otro medio. Para detener el seguimiento una vez que se ha alcanzado el límite de tamaño de archivo, deshabilite la opción de sustitución incremental de archivos.  
  
    > [!NOTE]  
    >  El sistema de archivos FAT32 limita los archivos a un poco menos de 4 GB. Cuando el archivo de seguimiento alcanza ese tamaño, el seguimiento se detiene con el error "Espacio insuficiente en disco". Para crear archivos de mayor tamaño, utilice el sistema de archivos NTFS.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  

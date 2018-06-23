---
title: Seleccionar dispositivo de copia de seguridad | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.selectbackupdevice.f1
ms.assetid: 7887c9fd-15ce-4cc8-b069-845c1d09088c
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6135239b182c66ae4622dcf9af704fb30f167f6f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109251"
---
# <a name="select-backup-device"></a>Seleccionar dispositivo de copia de seguridad
  Utilice el cuadro de diálogo **Seleccionar dispositivo lógico de copia de seguridad** para seleccionar un dispositivo de copia de seguridad para la operación de restauración.  
  
 Un dispositivo lógico de copia de seguridad es un dispositivo lógico definido por el usuario que corresponde a un dispositivo físico, ya sea una unidad de cinta o de disco, que proporciona el sistema operativo.  
  
> [!NOTE]  
>  Si una copia de seguridad utiliza varios dispositivos de copia de seguridad, todos deben corresponder a un solo tipo de dispositivo.  
  
 **Para utilizar SQL Server Management Studio a fin de ver el contenido de un dispositivo de copia de seguridad**  
  
-   [Ver el contenido de una cinta o un archivo de copia de seguridad &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opciones  
 **Dispositivo de copia de seguridad**  
 En el cuadro de lista, seleccione el nombre de un dispositivo lógico de copia de seguridad desde el que desea efectuar la restauración.  
  
 Para obtener información sobre cómo ver el contenido de un dispositivo de copia de seguridad, vea [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md).  
  
## <a name="remarks"></a>Notas  
 Si no ve un dispositivo lógico de copia de seguridad que contenga la copia de seguridad que busca en la lista, puede que dicha copia de seguridad se haya escrito directamente en uno o varios archivos o unidades de cinta. Si es así, cancele el cuadro de diálogo **Seleccionar dispositivo de copia de seguridad** ; en el cuadro de diálogo **Especificar copia de seguridad** , seleccione **Archivo** o **Cinta** en el cuadro de lista **Medio para copia de seguridad** .  
  
## <a name="see-also"></a>Vea también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md)  
  
  
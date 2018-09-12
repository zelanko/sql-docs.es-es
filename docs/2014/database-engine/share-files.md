---
title: Compartir archivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sharing files
- file sharing [SQL Server]
- version control services [SQL Server], file sharing
ms.assetid: 645f5c0a-e949-4e87-8988-85e4d6128464
caps.latest.revision: 20
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6da45eccfa103da171bfccc2e118e29b21566086
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43813211"
---
# <a name="share-files"></a>Compartir archivos
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] se puede utilizar para compartir elementos entre proyectos de control de código fuente. Cuando se comparte un elemento, los cambios realizados en éste se reflejan en todos los proyectos que comparten ese elemento.  
  
 El compartir elementos ofrece una serie de ventajas a los usuarios del control de código fuente:  
  
-   Hace innecesario que cada proyecto que utiliza el elemento compartido almacene una copia independiente del mismo, con lo que se ahorra espacio en disco tanto en el cliente como en el servidor de control de código fuente. El proveedor de control de código fuente almacena el elemento compartido en una ubicación central. Cada proyecto almacena un puntero a esa ubicación.  
  
-   Evita las incompatibilidades entre versiones. Puesto que cada proyecto que comparte el elemento utiliza la misma versión de éste, se evitan los conflictos que surgen cuando cada copia de un elemento cambia de forma independiente en varios proyectos.  
  
### <a name="to-share-an-item"></a>Para compartir un elemento  
  
1.  En el Explorador de soluciones, seleccione la carpeta o proyecto en que desea colocar los archivos compartidos.  
  
2.  En el **archivo** menú, elija **Control de código fuente**y, a continuación, haga clic en **Share**.  
  
3.  En el **compartir con** cuadro de diálogo Examinar la lista de directorios para el elemento que desea compartir y haga clic en ese elemento.  
  
4.  Haga clic en **Share**.  
  
## <a name="see-also"></a>Vea también  
 [Fundamentos del control de código fuente](../../2014/database-engine/source-control-basics.md)  
  
  

---
title: Compartir archivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- sharing files
- file sharing [SQL Server]
- version control services [SQL Server], file sharing
ms.assetid: 645f5c0a-e949-4e87-8988-85e4d6128464
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e779a0c0da9920b2efda5f52135e85f31959d10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62843561"
---
# <a name="share-files"></a>Compartir archivos
  
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] se puede utilizar para compartir elementos entre proyectos de control de código fuente. Cuando se comparte un elemento, los cambios realizados en éste se reflejan en todos los proyectos que comparten ese elemento.  
  
 El compartir elementos ofrece una serie de ventajas a los usuarios del control de código fuente:  
  
-   Hace innecesario que cada proyecto que utiliza el elemento compartido almacene una copia independiente del mismo, con lo que se ahorra espacio en disco tanto en el cliente como en el servidor de control de código fuente. El proveedor de control de código fuente almacena el elemento compartido en una ubicación central. Cada proyecto almacena un puntero a esa ubicación.  
  
-   Evita las incompatibilidades entre versiones. Puesto que cada proyecto que comparte el elemento utiliza la misma versión de éste, se evitan los conflictos que surgen cuando cada copia de un elemento cambia de forma independiente en varios proyectos.  
  
### <a name="to-share-an-item"></a>Para compartir un elemento  
  
1.  En el Explorador de soluciones, seleccione la carpeta o proyecto en que desea colocar los archivos compartidos.  
  
2.  En el menú **archivo** , seleccione **control de código fuente**y, a continuación, haga clic en **compartir**.  
  
3.  En el cuadro de diálogo **compartir con** , busque en la lista de directorios el elemento que desea compartir y haga clic en ese elemento.  
  
4.  Haga clic en **Compartir**.  
  
## <a name="see-also"></a>Consulte también  
 [Fundamentos del control de código fuente](../../2014/database-engine/source-control-basics.md)  
  
  

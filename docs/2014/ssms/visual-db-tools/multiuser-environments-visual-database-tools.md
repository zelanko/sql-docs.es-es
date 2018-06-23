---
title: Entornos multiusuario (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- users [SQL Server], multiuser environments
- conflict resolution [Visual Database Tools]
- multiple users making database changes
- multiuser environments [Visual Database Tools]
- database modifications [SQL Server]
- version control [Visual Database Tools]
- Visual Database Tools [SQL Server], multiuser environments
ms.assetid: 330bd48c-9427-4967-b58e-b7c492d5ee36
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 53b8335617a012c136a243d7b1063dac406195ac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204302"
---
# <a name="multiuser-environments-visual-database-tools"></a>Entornos multiusuario (Visual Database Tools)
  Un entorno multiusuario es un entorno al que otros usuarios pueden conectarse y en el que pueden realizar cambios en la misma base de datos en la que usted está trabajando. Como resultado, es posible que varios usuarios estén trabajando con los mismos objetos de base de datos a la vez. De este modo, en un entorno multiusuario es posible que la base de datos se vea afectada por los cambios realizados por otros usuarios mientras está trabajando y viceversa.  
  
 Una cuestión clave al trabajar con bases de datos en un entorno multiusuario son los permisos de acceso. Los permisos de que dispone para la base de datos determinan el alcance del trabajo que puede realizar con la base de datos. Por ejemplo, para realizar cambios en objetos en una base de datos, debe disponer de los permisos de escritura apropiados para la base de datos. Para obtener más información acerca de los permisos en la base de datos, vea la documentación de la base de datos. Para más información, consulte [Permisos y Visual Database Tools &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
 Cuando guarda los cambios realizados en las tablas, el Diseñador de tablas comprueba que la base de datos no se ha modificado desde que se guardaron los cambios por última vez. Si otro usuario ha realizado cambios, se le notificará que se ha modificado la base de datos. Es posible que necesite reconciliar estos cambios. Para más información, consulte [Reconciliar los cambios realizados por varios usuarios &#40;Visual Database Tools&#41;](reconcile-changes-made-by-multiple-users-visual-database-tools.md).  
  
 En un entorno multiusuario debe tenerse en cuenta consideraciones especiales para impedir que se produzcan conflictos en los cambios. Para más información, consulte [Problemas de evolución de bases de datos &#40;Visual Database Tools&#41;](issues-of-database-evolution-visual-database-tools.md).  
  
 Un modo de evitar problemas es trabajar con una copia de la base de datos, como una base de datos de prueba, cuando realiza los cambios; a continuación, puede crear un script y ejecutarlo para que aplique estos cambios en la base de datos original después de solucionar los conflictos sin conexión. Para más información, consulte [Bases de datos de desarrollo, pruebas y producción &#40;Visual Database Tools&#41;](development-test-and-production-databases-visual-database-tools.md).  
  
  
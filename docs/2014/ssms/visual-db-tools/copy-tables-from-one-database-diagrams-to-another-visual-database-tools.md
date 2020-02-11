---
title: Copiar tablas de un diagrama de base de datos a otro (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- copying tables
- duplicating tables
ms.assetid: 155a4f09-9321-4887-a7d4-aa2ce6b51277
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d1b0d70a5d8121963d424f25eef517af7cde4ba7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62720074"
---
# <a name="copy-tables-from-one-database-diagrams-to-another-visual-database-tools"></a>Copiar tablas de un diagrama de base de datos a otro (Visual Database Tools)
  Puede copiar una tabla de un diagrama de base de datos a otro de una misma base de datos.  
  
 Si copia una tabla de un diagrama de base de datos a otro, solo se agregará una referencia a la tabla del segundo diagrama. No se duplica la tabla en la base de datos. Por ejemplo, si copia la tabla `authors` de un diagrama de base de datos a otro, cada diagrama hará referencia a la misma tabla `authors` de la base de datos.  
  
### <a name="to-copy-a-table-from-another-database-diagram"></a>Para copiar una tabla de otro diagrama de base de datos  
  
1.  Asegúrese de que está conectado a la base de datos cuya tabla desea copiar.  
  
2.  Abra los diagramas de base de datos de origen y de destino y, en el diagrama de origen, seleccione la tabla que desea copiar al diagrama de destino.  
  
3.  Haga clic en el botón **Copiar** de la barra de herramientas. Esta acción coloca la definición de la tabla seleccionada en el Portapapeles.  
  
4.  Cambie al diagrama de destino. Este diagrama debe estar en la misma base de datos que el diagrama de origen.  
  
5.  Haga clic en el botón **Pegar** de la barra de herramientas. El contenido del Portapapeles aparecerá en la nueva ubicación y permanecerá resaltado hasta que haga clic en otro punto. Si existen relaciones entre las tablas seleccionadas y otras tablas del diagrama de destino, las líneas de las relaciones se dibujarán automáticamente.  
  
 Cuando edite la tabla en uno de los diagramas, los cambios se reflejarán en ambos. De forma similar, una vez guardada la tabla en cualquiera de los diagramas, la tabla ya no se considera "modificada" en ninguno de ellos.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con diagramas de base de datos &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Agregar tablas a diagramas &#40;Visual Database Tools&#41;](add-tables-to-diagrams-visual-database-tools.md)  
  
  

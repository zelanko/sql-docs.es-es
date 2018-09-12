---
title: Cuadro de diálogo Agregar tabla (Diseñador de bases de datos) (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65555
- vdt.dlgbox.schema.addtable
ms.assetid: 3c0b1b30-795c-4240-91d6-890b8348014a
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d6790aa4544ffde77ff30277b049ca9ed0b8e65d
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43820561"
---
# <a name="add-table-dialog-box-database-designer-visual-database-tools"></a>Agregar tabla (cuadro de diálogo, Visual Database Tools)
  Permite agregar tablas en el Diseñador de bases de datos.  
  
> [!NOTE]  
>  Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) u Objetos de administración de SQL Server (SMO). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Actualizar**  
 Actualiza la lista de tablas para que coincidan con el estado actual de la base de datos.  
  
 **Agregar**  
 Agrega las tablas seleccionadas.  
  
> [!NOTE]  
>  Si desea agregar varias tablas al diagrama, puede seleccionarlas todas antes de hacer clic en **Agregar**. Como alternativa, puede hacer doble clic en cada una de las tablas que desee agregar y, luego, hacer clic en **Cerrar** cuando termine.  
  
 **Cerrar**  
 Cierra el cuadro de diálogo sin agregar más tablas.  
  
## <a name="see-also"></a>Vea también  
 [Agregar tablas a diagramas &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  

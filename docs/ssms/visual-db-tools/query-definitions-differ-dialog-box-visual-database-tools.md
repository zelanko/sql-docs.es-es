---
title: "Cuadro de diálogo Definiciones de consulta diferentes (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:69639
- vdtsql.chm:69640
- vdt.dlgbox.querydefinitionsdiffer
ms.assetid: 90383473-2922-40e5-9682-3850849aa856
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 630593a904b4fb28e39e94a81e02481c0e6a8e1d
ms.contentlocale: es-es
ms.lasthandoff: 08/18/2017

---
# <a name="query-definitions-differ-dialog-box-visual-database-tools"></a>Definiciones de consulta diferentes (cuadro de diálogo, Visual Database Tools)
Este cuadro de diálogo notifica que no se puede representar gráficamente la consulta en los paneles Diagrama y Criterios, y que solo se puede modificar la consulta en el panel SQL.  
  
Este cuadro de diálogo puede aparecer cuando escriba o modifique una instrucción SQL en el panel SQL; a continuación, si se desplaza a otro panel, comprueba la consulta o intenta ejecutarla, se producirá una de las siguientes situaciones:  
  
-   La instrucción SQL no está completa o contiene uno o varios errores de sintaxis.  
  
-   La instrucción SQL es válida, pero no se admite en los paneles gráficos (por ejemplo, una consulta Union).  
  
-   La instrucción SQL es válida, pero contiene una sintaxis específica de la conexión de datos utilizada.  
  
> [!TIP]  
> Puede comprobar la validez de una instrucción mediante el botón **Comprobar instrucción SQL** de la barra de herramientas **Consulta** .  
  
El cuadro de diálogo muestra un mensaje que indica el motivo por el que no se puede representar la instrucción SQL y, a continuación, le pregunta qué desea hacer.  
  
> [!NOTE]  
> Si los paneles Diagrama y Criterios están ocultos, el cuadro de diálogo **Definiciones de consulta diferentes** no aparecerá.  
  
## <a name="options"></a>Opciones  
**Omitir (Botón)**  
Haga clic en este botón para especificar que desea aceptar la instrucción SQL, con el fin de ejecutarla o realizar una nueva modificación. Si acepta la instrucción, los paneles Diagrama y Criterios se mostrarán atenuados para indicar que no representan la instrucción en el panel SQL.  
  
**Deshacer (Botón)**  
Haga clic en este botón para descartar los cambios realizados en el panel SQL.  
  
> [!NOTE]  
> Si la instrucción es correcta, pero el Diseñador de consultas y vistas no la admite gráficamente, podrá ejecutarla aunque no se pueda representar en los paneles Diagrama y Criterios. Por ejemplo, si indica una consulta de unión, se podrá ejecutar la instrucción, pero no se podrá representar en los otros paneles.  
  
## <a name="see-also"></a>Vea también  
[Herramientas Diseñador de consultas y vistas (Visual Database Tools)](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)  
  


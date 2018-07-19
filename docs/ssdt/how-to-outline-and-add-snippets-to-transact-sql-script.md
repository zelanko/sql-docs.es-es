---
title: Esquematización y adición de fragmentos de código a script Transact-SQL | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 543e7ce7-8639-4281-8a91-85314755e5de
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b08337c4602e7eaad2da376b22caa8f806e5b18
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094621"
---
# <a name="how-to-outline-and-add-snippets-to-transact-sql-script"></a>Cómo: Esquematizar y agregar fragmentos de código a script Transact-SQL
SQL Server Data Tools incluye una biblioteca de código formada por fragmentos de código que están listos para insertarse en la aplicación. Cada fragmento de código realiza una tarea de script completa como la creación de una función, tabla, desencadenador, índice, vista, tipo de datos definido por el usuario, etc. Bastan unos pocos clics del mouse para insertar un fragmento de código en el código fuente. Estos fragmentos de código aumentan la productividad al reducir el tiempo dedicado a escribir.  
  
Si necesita buscar un fragmento de código adecuado, puede usar el selector de fragmentos de código, que proporciona listas clasificadas por categorías de fragmentos de código entre las que puede elegir. Una vez agregado el fragmento de código al código, puede que haya que personalizar algunas partes del mismo, como reemplazar nombres de variable con nombres más apropiados o poner la lógica real de un procedimiento almacenado. Observará que el fragmento de código insertado contiene uno o varios puntos de reemplazo resaltados en el código para este fin. Si sitúa el puntero del mouse sobre el punto de reemplazo, aparecerá una información sobre herramientas en la que se explica cómo puede cambiar el código.  
  
De forma predeterminada, todo el texto se muestra en el Editor de Transact\-SQL, pero puede hacer que no se vea parte del mismo. El Editor de Transact\-SQL permite seleccionar una región de código y hacerla contraíble, de forma que aparezca bajo un signo más (+). Se puede expandir u ocultar la región haciendo clic en el signo más (+) situado junto al símbolo. El código esquematizado no se elimina; simplemente se oculta.  
  
> [!WARNING]  
> Los procedimientos siguientes usan entidades creadas en procedimientos anteriores de las secciones [Desarrollo de bases de datos conectadas](../ssdt/connected-database-development.md) y [Desarrollo de bases de datos sin conexión orientado a proyectos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-insert-snippets"></a>Para insertar fragmentos de código  
  
1.  Haga clic con el botón secundario en el proyecto **TradeDev** en el **Explorador de soluciones**, seleccione **Agregar** y, a continuación, haga clic en **Script**. En el cuadro de diálogo **Agregar nuevo elemento**, haga clic en **Agregar**.  
  
2.  Haga clic con el botón derecho en el Editor de Transact\-SQL y seleccione **Insertar fragmento de código**. Aparecerá el selector de fragmentos de código.  
  
3.  Haga doble clic en **Tabla** en el selector de fragmentos de código y, a continuación, haga doble clic en **Crear tabla**.  
  
4.  Observe que los puntos de reemplazo están resaltados en amarillo. Mantenga el mouse sobre `Sample_Table` y una información sobre herramientas mostrará una descripción del reemplazo. Haga doble clic en `Sample_Table` y cámbielo a `Shipper2`.  
  
5.  Use la tecla TAB para pasar al siguiente punto de reemplazo, que es `column_1`. Cambie su nombre a `Id`. Siga los mismos pasos para cambiar el nombre de `column_2` a `name`, cambie su tipo de datos a `nvarchar(128)` y permita valores `NULL`.  
  
### <a name="to-outline-code"></a>Para esquematizar código  
  
1.  Observe el signo **–** situado junto a la instrucción CREATE TABLE. Haga clic en el signo **-** situado junto a una sección del script para ocultarla.  
  
2.  Haga clic con el botón secundario en el Editor de Transact\-SQL y seleccione **Esquematización**; después, seleccione **Detener esquematización** para quitar la información de esquema sin afectar al código subyacente del editor.  
  
3.  Para empezar a esquematizar el código de nuevo, haga clic con el botón secundario en el Editor de Transact\-SQL, seleccione **Esquematización** y, a continuación, seleccione **Iniciar esquematización automática**. También puede seleccionar **Alternar toda la esquematización** para cambiar entre expandir y ocultar secciones.  
  

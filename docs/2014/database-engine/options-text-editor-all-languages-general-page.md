---
title: Opciones (editor de texto-todos los lenguajes-página general) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: bf18907c-94e2-4c09-9b2b-0925ac04c627
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 385380e6e51c3b8519e7dbc6ec3d934e1ef14846
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089249"
---
# <a name="options-text-editor---all-languages---general-page"></a>Opciones (Editor de texto - Todos los idiomas - Página General)
  Utilice este cuadro de diálogo para establecer opciones generales de edición en los cinco editores de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para mostrar estas opciones, haga clic en **Opciones** en el menú **Herramientas** . Seleccione la carpeta **Editor de texto** , expanda la carpeta **Todos los lenguajes** y haga clic en **General**.  
  
## <a name="option-settings-by-editor"></a>Configuración de las opciones de editor  
 Debe usar los cuadros de diálogo de **Todos los lenguajes** para establecer las opciones de los editores DMX, MDX y SQL Server Compact. Las opciones establecidas aquí también se aplican al texto simple, a Transact-SQL y a los editores XML, pero puede establecer opciones por separado para esos editores si expande las subcarpetas correspondientes a esos idiomas y selecciona sus páginas de opciones.  
  
> [!CAUTION]  
>  Si establece la opción usar este cuadro de diálogo, pero quiere un valor diferente para el texto simple, Transact-SQL o el editor XML, debe establecer las opciones de esos editores después de aplicar las opciones seleccionadas en el cuadro de diálogo **Todos los lenguajes**.  
  
 Algunos editores pueden no admitir todas las opciones incluidas en esta página. Si una opción de la página **General** del cuadro de diálogo **Opciones** se ha seleccionado para algunos lenguajes de programación pero no para otros, aparece una marca de verificación sombreada.  
  
## <a name="statement-completion"></a>Finalización de instrucciones  
 **Lista de miembros automática**  
 Muestra listas emergentes de miembros, propiedades o valores disponibles a medida que escribe en el editor. Elija cualquier elemento de la lista emergente para insertarlo en el código. Si activa esta casilla, se habilita la opción **Ocultar miembros avanzados** .  
  
 **Ocultar miembros avanzados**  
 Reduce las listas emergentes de finalización de instrucciones reducidas y muestra solo los elementos de uso más frecuente. Los demás elementos se extraen de la lista. Esta opción no está disponible si no existen miembros marcados como miembros avanzados.  
  
 **Información de parámetros**  
 Muestra la sintaxis completa para la declaración o procedimiento actual a la izquierda del punto de inserción del editor, con todos sus parámetros disponibles. El siguiente parámetro que puede asignar aparece en negrita.  
  
## <a name="settings"></a>Configuración  
 **Habilitar espacio virtual**  
 Permite colocar comentarios en un punto coherente junto al código. Si activa esta casilla, puede colocar el cursor después del último carácter de la fila. Cuando se escribe, se agregan tabuladores o espacios de forma automática para completar la fila hasta el punto de inserción.  
  
 **Ajuste de palabra**  
 Muestra, en la siguiente línea, cualquier parte de una línea que se extienda horizontalmente fuera del área visible del editor. Cuando se selecciona esta casilla, se habilita la opción **Mostrar glifos visuales para ajuste de línea** .  
  
 **Mostrar glifos visuales para ajuste de línea**  
 Muestra un indicador de retorno de carro donde una línea larga se haya ajustado a una segunda línea.  
  
> [!NOTE]  
>  Estas flechas de recordatorio no se agregan al código y no se imprimen. Solo sirven como referencia. Esta característica no está disponible en todos los tipos de editores.  
  
 **Aplicar comandos Cortar o Copiar a líneas en blanco si no hay selección**  
 Establece el comportamiento del editor cuando el punto de inserción se coloca en una línea en blanco, no se selecciona nada y se hace clic en **Copiar** o **Cortar**.  
  
 Cuando se selecciona esta casilla, se copia o se corta la línea en blanco. Si luego hace clic en **Pegar**, se insertará una nueva línea en blanco.  
  
 Cuando esta casilla está desactivada, no se copia o se corta nada. Si luego hace clic en **Pegar**, se pegará el contenido de la última copia. Si previamente no se ha copiado nada, no se pegará nada.  
  
 Este parámetro no afecta a los comandos **Copiar** ni **Cortar** cuando la línea no está en blanco. Si no se selecciona nada, se copia o se corta la línea entera. Si luego hace clic en **Pegar**, se pegará el texto de toda la línea y su carácter de final de línea.  
  
## <a name="display"></a>Pantalla  
 **Números de línea**  
 Muestra un número de línea junto a cada línea de código.  
  
> [!NOTE]  
>  Estos números de línea no se agregan al código y no se imprimen. Solo sirven como referencia.  
  
 **Habilitar acceso a direcciones URL con un solo clic**  
 El cursor cambia a un símbolo de mano cuando pasa por encima de una dirección URL en el editor. Puede hacer clic en la dirección URL para abrir la página indicada en el explorador web.  
  
 **Barra de navegación**  
 Muestra una barra de navegación en la parte superior del Editor de código. Use sus listas desplegables **Objetos** y **Procedimientos** para elegir un objeto determinado en el código, seleccionar en sus procedimientos e insertar una instancia del procedimiento seleccionado. La barra de navegación no está disponible en todos los tipos de código.  
  
  

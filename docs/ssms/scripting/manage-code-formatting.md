---
title: Administración de formato de código | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- indenting code [SQL Server]
- displaying URLs
- code formatting [SQL Server Management Studio]
- collapsing text
- formats [SQL Server], code formatting in SQL Server Management Studio
- hiding text
- formats [SQL Server]
- text [SQL Server], code formats
- automatic indentation
- converting text to lower case
- Query Editor [SQL Server Management Studio], managing code formats
- URL displayed in code [SQL Server Management Studio]
- converting text to upper case
- text [SQL Server]
- unindenting code
ms.assetid: ddbac4d2-6bdc-4467-a352-e869ec880eed
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b80668cadd7ea2b2b721f93d41c79a08290c3370
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65821976"
---
# <a name="manage-code-formatting"></a>Administrar formato de código
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Con el editor, puede aplicar formato al código mediante sangrías, texto oculto, direcciones URL, etc. También se puede aplicar formato al código automáticamente a medida que se escribe mediante sangrías automáticas.  
  
## <a name="indenting"></a>Sangrías  
 Puede optar entre tres estilos diferentes de sangría de texto. También puede especificar cuántos espacios componen una única sangría o tabulación, y si el editor utiliza tabulaciones o caracteres de espacio al aplicar sangrías.  
  
#### <a name="to-choose-an-indenting-style"></a>Para elegir un estilo de sangría  
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  Haga clic en **Editor de texto**.  
  
3.  Seleccione **Todos los lenguajes** para establecer la sangría para todos los lenguajes.  
  
4.  Haga clic en **Tabulaciones**.  
  
5.  Haga clic en una de las opciones siguientes:  
  
    -   **Ninguna**. El cursor va al comienzo de la línea siguiente.  
  
    -   **Bloque**. El cursor alinea la línea siguiente con la anterior.  
  
    -   **Inteligente** (valor predeterminado). El servicio de lenguaje determina el estilo de sangría adecuado.  
  
    > [!NOTE]  
    >  Algunos lenguajes no ofrecen las tres opciones de sangría.  
  
#### <a name="to-change-indent-tab-settings"></a>Para cambiar la configuración de las tabulaciones  
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  Haga clic en **Editor de texto**.  
  
3.  Seleccione **Todos los lenguajes** para establecer la sangría para todos los lenguajes.  
  
4.  Haga clic en **Tabulaciones**.  
  
5.  Para especificar caracteres de tabulación para las operaciones con tabulaciones y sangrías, haga clic en **Mantener tabulaciones**. Para especificar caracteres de espacio, seleccione **Insertar espacios**.  
  
     Si selecciona **Insertar espacios**, especifique el número de caracteres que representa cada tabulador o sangría en **Tamaño de tabulación** o **Tamaño de sangría**, respectivamente.  
  
#### <a name="to-indent-code"></a>Para aplicar sangría al código  
  
1.  Seleccione el texto al que desea aplicar sangría.  
  
2.  Presione la tecla TAB o haga clic en el botón **Aplicar sangría** de la barra de herramientas Estándar.  
  
#### <a name="to-unindent-code"></a>Para quitar la sangría del código  
  
1.  Seleccione el texto cuya sangría desea quitar.  
  
2.  Pulse MAYÚS+TAB o haga clic en el botón **Quitar sangría** de la barra de herramientas Estándar.  
  
#### <a name="to-automatically-indent-all-of-your-code"></a>Para aplicar sangría automáticamente a todo el código  
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  Haga clic en **Editor de texto**.  
  
3.  Haga clic en **Todos los lenguajes**.  
  
4.  Haga clic en **Tabulaciones**.  
  
5.  Haga clic en **Automática**.  
  
> [!NOTE]  
>  La opción **Inteligente** no está disponible en algunos lenguajes.  
  
#### <a name="to-convert-white-space-to-tabs"></a>Para convertir espacios en blanco en tabulaciones  
  
1.  Seleccione el texto cuyos espacios en blanco desea convertir en tabulaciones.  
  
2.  En el menú **Editar** , elija **Avanzado**y, a continuación, haga clic en **Aplicar tabulaciones a la selección**.  
  
#### <a name="to-convert-tabs-to-spaces"></a>Para convertir tabulaciones en espacios  
  
1.  Seleccione el texto cuyas tabulaciones desea convertir en espacios.  
  
2.  En el menú **Editar** , elija **Avanzado**y, a continuación, haga clic en **No aplicar tabulaciones a la selección**.  
  
 El comportamiento de estos comandos depende de la configuración de las tabulaciones en el cuadro de diálogo **Opciones** . Por ejemplo, si la configuración de las tabulaciones es 4, **Aplicar tabulaciones a la selección** crea una tabulación por cada 4 espacios contiguos. Mientras, **No aplicar tabulaciones a la selección** crea 4 espacios por cada tabulación.  
  
## <a name="converting-text-to-upper-and-lower-case"></a>Convertir texto en mayúsculas y minúsculas  
 Puede utilizar comandos para convertir texto en mayúsculas o minúsculas.  
  
#### <a name="to-switch-text-to-upper-or-lower-case"></a>Para alternar texto en mayúsculas o minúsculas  
  
1.  Seleccione el texto que desea convertir.  
  
2.  Para convertir texto en mayúsculas, pulse CTRL+MAYÚS+U o haga clic en **Poner en mayúsculas** en el submenú **Avanzado** del menú **Editar** .  
  
3.  Para convertir texto en minúsculas, pulse CTRL+MAYÚS+L o haga clic en **Poner en minúsculas** en el submenú **Avanzado** del menú **Editar** .  
  
> [!NOTE]  
>  Para obtener una lista completa de las teclas de método abreviado, vea [Métodos abreviados de teclado de SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md).  
  
## <a name="displaying-and-linking-to-urls"></a>Mostrar direcciones URL y crear vínculos  
 En el código, puede crear y mostrar direcciones URL en las que se puede hacer clic. De manera predeterminada, las direcciones URL:  
  
-   Están subrayadas.  
  
-   Cambian el puntero del mouse (ratón) a una mano cuando pasa por encima.  
  
-   Si la dirección es válida, abren la dirección URL al hacer clic.  
  
#### <a name="to-display-a-clickable-url"></a>Para mostrar una dirección URL en la que se puede hacer clic  
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  Haga clic en **Editor de texto**.  
  
3.  Para cambiar la opción para un único lenguaje, haga clic en la carpeta de ese lenguaje y, a continuación, en **General**. Para cambiar la opción para todos los lenguajes, haga clic en **Todos los lenguajes** y, a continuación, en **General**.  
  
4.  Active **Habilitar la navegación a direcciones URL con un solo clic**.  
  
  

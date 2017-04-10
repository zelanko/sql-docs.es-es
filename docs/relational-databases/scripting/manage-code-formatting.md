---
title: "Administrar formato de c&#243;digo | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "aplicar sangría al código [SQL Server]"
  - "mostrar direcciones URL"
  - "formato de código [SQL Server Management Studio]"
  - "contraer texto"
  - "formatos [SQL Server], formato de código en SQL Server Management Studio"
  - "ocultar texto"
  - "formatos [SQL Server]"
  - "texto [SQL Server], formatos de código"
  - "sangría automática"
  - "convertir texto en minúsculas"
  - "Editor de consultas [SQL Server Management Studio], administrar formatos de código"
  - "dirección URL del código [SQL Server Management Studio]"
  - "convertir texto en mayúsculas"
  - "texto [SQL Server]"
  - "quitar la sangría del código"
ms.assetid: ddbac4d2-6bdc-4467-a352-e869ec880eed
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Administrar formato de c&#243;digo
  Con el editor, puede aplicar formato al código mediante sangrías, texto oculto, direcciones URL, etc. También se puede aplicar formato al código automáticamente a medida que se escribe mediante sangrías automáticas.  
  
## Sangrías  
 Puede optar entre tres estilos diferentes de sangría de texto. También puede especificar cuántos espacios componen una única sangría o tabulación, y si el editor utiliza tabulaciones o caracteres de espacio al aplicar sangrías.  
  
#### Para elegir un estilo de sangría  
  
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
  
#### Para cambiar la configuración de las tabulaciones  
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  Haga clic en **Editor de texto**.  
  
3.  Seleccione **Todos los lenguajes** para establecer la sangría para todos los lenguajes.  
  
4.  Haga clic en **Tabulaciones**.  
  
5.  Para especificar caracteres de tabulación para las operaciones con tabulaciones y sangrías, haga clic en **Mantener tabulaciones**. Para especificar caracteres de espacio, seleccione **Insertar espacios**.  
  
     Si selecciona **Insertar espacios**, especifique el número de caracteres que representa cada tabulador o sangría en **Tamaño de tabulación** o **Tamaño de sangría**, respectivamente.  
  
#### Para aplicar sangría al código  
  
1.  Seleccione el texto al que desea aplicar sangría.  
  
2.  Presione la tecla TAB o haga clic en el botón **Aplicar sangría** de la barra de herramientas Estándar.  
  
#### Para quitar la sangría del código  
  
1.  Seleccione el texto cuya sangría desea quitar.  
  
2.  Pulse MAYÚS+TAB o haga clic en el botón **Quitar sangría** de la barra de herramientas Estándar.  
  
#### Para aplicar sangría automáticamente a todo el código  
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  Haga clic en **Editor de texto**.  
  
3.  Haga clic en **Todos los lenguajes**.  
  
4.  Haga clic en **Tabulaciones**.  
  
5.  Haga clic en **Automática**.  
  
> [!NOTE]  
>  La opción **Inteligente** no está disponible en algunos lenguajes.  
  
#### Para convertir espacios en blanco en tabulaciones  
  
1.  Seleccione el texto cuyos espacios en blanco desea convertir en tabulaciones.  
  
2.  En el menú **Editar** , elija **Avanzado**y, a continuación, haga clic en **Aplicar tabulaciones a la selección**.  
  
#### Para convertir tabulaciones en espacios  
  
1.  Seleccione el texto cuyas tabulaciones desea convertir en espacios.  
  
2.  En el menú **Editar** , elija **Avanzado**y, a continuación, haga clic en **No aplicar tabulaciones a la selección**.  
  
 El comportamiento de estos comandos depende de la configuración de las tabulaciones en el cuadro de diálogo **Opciones** . Por ejemplo, si la configuración de las tabulaciones es 4, **Aplicar tabulaciones a la selección** crea una tabulación por cada 4 espacios contiguos. Mientras, **No aplicar tabulaciones a la selección** crea 4 espacios por cada tabulación.  
  
## Convertir texto en mayúsculas y minúsculas  
 Puede utilizar comandos para convertir texto en mayúsculas o minúsculas.  
  
#### Para alternar texto en mayúsculas o minúsculas  
  
1.  Seleccione el texto que desea convertir.  
  
2.  Para convertir texto en mayúsculas, pulse CTRL+MAYÚS+U o haga clic en **Poner en mayúsculas** en el submenú **Avanzado** del menú **Editar**.  
  
3.  Para convertir texto en minúsculas, pulse CTRL+MAYÚS+L o haga clic en **Poner en minúsculas** en el submenú **Avanzado** del menú **Editar**.  
  
> [!NOTE]  
>  Para obtener una lista completa de las teclas de método abreviado, vea [Métodos abreviados de teclado de SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md).  
  
## Mostrar direcciones URL y crear vínculos  
 En el código, puede crear y mostrar direcciones URL en las que se puede hacer clic. De manera predeterminada, las direcciones URL:  
  
-   Están subrayadas.  
  
-   Cambian el puntero del mouse (ratón) a una mano cuando pasa por encima.  
  
-   Si la dirección es válida, abren la dirección URL al hacer clic.  
  
#### Para mostrar una dirección URL en la que se puede hacer clic  
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  Haga clic en **Editor de texto**.  
  
3.  Para cambiar la opción para un único lenguaje, haga clic en la carpeta de ese lenguaje y, a continuación, en **General**. Para cambiar la opción para todos los lenguajes, haga clic en **Todos los lenguajes** y, a continuación, en **General**.  
  
4.  Active **Habilitar la navegación a direcciones URL con un solo clic**.  
  
  
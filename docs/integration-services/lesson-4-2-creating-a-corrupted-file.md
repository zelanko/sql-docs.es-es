---
title: 'Paso 2: Creación de un archivo dañado | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9805a1d1fd1c6e025ee7ddb83c7241037dbae30b
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58273360"
---
# <a name="lesson-4-2-create-a-corrupted-file"></a>Lección 4-2: Creación de un archivo dañado

Para demostrar la configuración y el control de los errores de transformación, necesita un archivo plano de ejemplo que, cuando se procese, genere un error en un componente.  
  
En esta tarea, se crea una copia de un archivo plano de ejemplo existente. Después, el archivo se abre en el Bloc de notas y se modifica la columna **CurrencyID** para que contenga un valor erróneo, lo que produce un error en la búsqueda. Cuando se procesa el archivo dañado, el error de búsqueda hace que se produzca un error en la transformación de búsqueda Currency Key y, por tanto, en el resto del paquete. Una vez que haya creado el archivo de ejemplo dañado, ejecute el paquete para ver su error.  
  
## <a name="create-a-corrupted-sample-flat-file"></a>Creación de un archivo plano de ejemplo dañado  
  
1.  En el Bloc de notas o en cualquier otro editor de texto, abra el archivo **Currency_VEB.txt**.  
  
2.  Utilice la función de búsqueda y sustitución del editor de texto para buscar todas las instancias de **VEB** y sustituirlas por **BAD**.  
  
3.  Guarde el archivo modificado en la misma carpeta que los otros archivos de datos de ejemplo con el nombre **Currency_BAD.txt**.  
  
    > [!NOTE]  
    > Asegúrese de que **Currency_BAD.txt** se guarde en la misma carpeta que los demás archivos de datos de ejemplo.  
  
4.  Cierre el editor de texto.  
  
## <a name="verify-that-an-error-occurs-during-run-time"></a>Comprobación de que se produce un error durante la ejecución  
  
1.  En el menú **Depurar**, seleccione **Iniciar depuración**.  
  
    En la tercera iteración del flujo de datos, la transformación Lookup Currency Key intenta procesar el archivo **Currency_BAD.txt** y la transformación genera un error. El error de la transformación hace que todo el paquete genere un error.  
  
2.  En el menú **Depurar**, seleccione **Detener depuración**.  
  
3.  En la superficie de diseño, haga clic en la pestaña **Resultados de la ejecución**.  
  
4.  Examine el registro y compruebe que se ha producido el siguiente error no controlado:  
  
    ```
    [Lookup Currency Key[27]] Error: Row yielded no match during lookup.
    ```
  
    > [!NOTE]  
    > El número 27 es el Id. del componente. Este valor se asigna al generar el flujo de datos, y es posible que el valor del paquete sea diferente.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente  
[Paso 3: Adición de redireccionamiento de flujo de errores](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
  
  

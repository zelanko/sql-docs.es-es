---
title: 'Paso 2: Crear un archivo dañado | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b77bcdee3a2382bef57d6b8c2ceb791da983d399
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2018
ms.locfileid: "51637572"
---
# <a name="lesson-4-2---creating-a-corrupted-file"></a>Lección 4-2: Crear un archivo dañado
Para demostrar los errores de configuración y el control de los errores de transformación, debe crear un archivo plano de ejemplo que, cuando se procese, genere un error en un componente.  
  
En esta tarea, creará una copia de un archivo plano de ejemplo existente. Luego abrirá el archivo en el Bloc de notas y modificará la columna **CurrencyID** para garantizar que no pueda producir una coincidencia durante la búsqueda de transformaciones. Cuando se procese el archivo nuevo, el error de búsqueda hará que se produzca un error en la transformación Lookup Currency Key y, por consiguiente, el resto del paquete generará un error. Una vez que haya creado el archivo de ejemplo dañado, ejecutará el paquete para ver su error.  
  
### <a name="to-create-a-corrupted-sample-flat-file"></a>Para crear un archivo plano de ejemplo dañado  
  
1.  En el Bloc de notas o en cualquier otro editor de texto, abra el archivo Currency_VEB.txt.  
  
    Los datos de ejemplo se incluyen con los paquetes de lecciones de SSIS. Para descargar los datos de ejemplo y los paquetes de lecciones, haga lo siguiente.  
  
    1.  Navegue a los [ejemplos del producto Integration Services](https://go.microsoft.com/fwlink/?LinkID=267527).  
  
    2.  Haga clic en la pestaña **DOWNLOADS** .  
  
    3.  Haga clic en el archivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
2.  Utilice la función de búsqueda y sustitución del editor de texto para buscar todas las instancias de **VEB** y sustituirlas por **BAD**.  
  
3.  Guarde el archivo modificado en la misma carpeta que los otros archivos de datos de ejemplo con el nombre **Currency_BAD.txt**.  
  
    > [!IMPORTANT]  
    > Asegúrese de que **Currency_BAD.txt** se guarde en la misma carpeta que los demás archivos de datos de ejemplo.  
  
4.  Cierre el editor de texto.  
  
### <a name="to-verify-that-an-error-will-occur-during-run-time"></a>Para comprobar que se producirá un error durante la ejecución  
  
1.  En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
    En la tercera iteración del flujo de datos, la transformación Lookup Currency Key intenta procesar el archivo Currency_BAD.txt y la transformación generará un error. El error de la transformación hará que todo el paquete genere un error.  
  
2.  En el menú **Depurar** , haga clic en **Detener depuración**.  
  
3.  En la superficie de diseño, haga clic en la pestaña **Resultados de la ejecución** .  
  
4.  Examine el registro y compruebe que se ha producido el siguiente error no controlado:  
  
    `[Lookup Currency Key[27]] Error: Row yielded no match during lookup.`  
  
    > [!NOTE]  
    > El número 27 es el Id. del componente. Este valor se asigna al generar el flujo de datos, y es posible que el valor del paquete sea diferente.  
  
## <a name="next-steps"></a>Next Steps  
[Paso 3: Agregar redirección de flujo de errores](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
  
  

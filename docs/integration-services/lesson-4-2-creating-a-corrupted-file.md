---
title: "Paso 2: Crear un archivo dañado | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7760a481839ec7bd33aeeefd4b066f3d7750020d
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-4-2---creating-a-corrupted-file"></a>Lección 4: 2: crear un archivo dañado
Para demostrar los errores de configuración y el control de los errores de transformación, debe crear un archivo plano de ejemplo que, cuando se procese, genere un error en un componente.  
  
En esta tarea, creará una copia de un archivo plano de ejemplo existente. Luego abrirá el archivo en el Bloc de notas y modificará la columna **CurrencyID** para garantizar que no pueda producir una coincidencia durante la búsqueda de transformaciones. Cuando se procese el archivo nuevo, el error de búsqueda hará que se produzca un error en la transformación Lookup Currency Key y, por consiguiente, el resto del paquete generará un error. Una vez que haya creado el archivo de ejemplo dañado, ejecutará el paquete para ver su error.  
  
### <a name="to-create-a-corrupted-sample-flat-file"></a>Para crear un archivo plano de ejemplo dañado  
  
1.  En el Bloc de notas o en cualquier otro editor de texto, abra el archivo Currency_VEB.txt.  
  
    Los datos de ejemplo se incluyen con los paquetes de lecciones de SSIS. Para descargar los datos de ejemplo y los paquetes de lecciones, haga lo siguiente.  
  
    1.  Navegue a los [ejemplos del producto Integration Services](http://go.microsoft.com/fwlink/?LinkID=267527).  
  
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
  
## <a name="next-steps"></a>Pasos siguientes  
[Paso 3: Agregar redirección de flujo de errores](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
  
  


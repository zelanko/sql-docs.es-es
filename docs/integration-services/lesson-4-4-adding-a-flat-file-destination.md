---
title: 'Paso 4: Adición de un destino de archivo plano | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f4088de3-16d8-419c-96a1-a2cd005d0a5b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 55c040385615c0bd7db750f7eb31a0f2eb7aa73b
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58273843"
---
# <a name="lesson-4-4-add-a-flat-file-destination"></a>Lección 4-4: Adición de un destino de archivo plano

La salida de errores de la transformación Lookup Currency Key redirige todas las filas de datos que hayan generado un error durante la búsqueda a la transformación Script. Para proporcionar más información sobre los errores producidos, la transformación Script ejecuta un script que obtiene una descripción de cada error.  
  
En esta tarea, guardará toda esta información sobre las filas con errores en un archivo de texto delimitado para su procesamiento posterior. Para guardar las filas con error, se agrega y configura un administrador de conexiones de archivos planos para el archivo de texto que contiene los datos de error y un destino de archivo plano. Al establecer propiedades en el administrador de conexiones de archivos planos que usa el destino de archivo plano, puede especificar la manera en que el destino de archivo plano establece el formato y escribe el archivo de texto. Para más información, vea [Administrador de conexiones de archivos planos](../integration-services/connection-manager/flat-file-connection-manager.md) y [Destino de archivo plano](../integration-services/data-flow/flat-file-destination.md).  
  
## <a name="add-and-configure-a-flat-file-destination"></a>Adición y configuración de un destino de archivo plano  
  
1.  Haga clic en la pestaña **Flujo de datos**.  
  
2.  En el **Cuadro de herramientas de SSIS**, expanda **Otros destinos** y arrastre **Destino de archivo plano** a la superficie de diseño del flujo de datos. Coloque el **Destino de archivo plano** directamente debajo de la transformación **Get Error Description** .  
  
3.  Haga clic en la transformación **Get Error Description** y, después, arrastre la flecha de color azul hasta el nuevo **Destino de archivo plano**.  
  
4.  En la superficie de diseño **Flujo de datos**, haga clic en el nombre **Destino de archivo plano** en la nueva transformación **Destino de archivo plano** y cambie el nombre a **Failed Rows**.  
  
5.  Haga clic con el botón derecho en la transformación **Failed Rows**, haga clic en **Editar** y, después, en el **Editor de destino de archivos planos**, haga clic en **Nuevo**.  
  
6.  En el cuadro de diálogo **Formato de archivo plano**, compruebe que esté seleccionado **Delimitado** y haga clic en **Aceptar**.  
  
7.  En el cuadro **Nombre del administrador de conexiones** del **Editor del administrador de conexiones de archivos planos**, escriba *Error Data*.  
  
8.  En el cuadro de diálogo **Editor del administrador de conexiones de archivos planos**, haga clic en **Examinar** y busque la carpeta en la que se va a almacenar el archivo.  
  
9. En el cuadro de diálogo **Abrir**, en **Nombre de archivo**, escriba *ErrorOutput.txt* y haga clic en **Abrir**.  
  
10. En el cuadro de diálogo **Editor del administrador de conexiones de archivos planos**, compruebe que el cuadro **Configuración regional** es **Inglés (Estados Unidos)** y la **Página de códigos** es **1252 (ANSI-Latin I)**.  
  
11. En el panel de opciones, haga clic en **Columnas**.  
  
    Además de las columnas del archivo de datos de origen, existen tres columnas nuevas: ErrorCode, ErrorColumn y ErrorDescription. Estas columnas son la salida de errores de la transformación Lookup Currency Key y el script de la transformación Get Error Description. Se pueden usar para solucionar el problema de la fila que genera el error.  
  
12. Seleccione **Aceptar**.  
  
13. En el **Editor de destino de archivos planos**, desactive la casilla **Sobrescribir los datos del archivo** .  
  
    Al desactivar esta casilla, se conservan los errores sobre múltiples ejecuciones del paquete mediante la anexión la salida de errores a cada ejecución nueva.
  
14. En el **Editor de destino de archivos planos**, haga clic en **Asignaciones** para comprobar que todas las columnas son correctas. Si lo desea, puede cambiar el nombre de las columnas en el destino.  
  
15. Seleccione **Aceptar**.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente
[Paso 5: Prueba del paquete del tutorial de la lección 4](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
  
  

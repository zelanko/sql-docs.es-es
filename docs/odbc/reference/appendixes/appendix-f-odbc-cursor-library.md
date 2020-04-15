---
title: 'Apéndice F: Biblioteca de cursores ODBC Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec7982150bfa805c7093ab445400ef5ad1ee070c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292435"
---
# <a name="appendix-f-odbc-cursor-library"></a>Apéndice F: Biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 La biblioteca de cursores ODBC (Odbccr32.dll) admite cursores desplazables de bloque para cualquier controlador que cumpla con el nivel de conformidad de la API de nivel 1 y pueda ser redistribuido por los desarrolladores con sus aplicaciones o controladores. La biblioteca de cursores también admite instrucciones de actualización y eliminación posicionadas para conjuntos de resultados generados por instrucciones **SELECT.** Aunque solo admite cursores estáticos y de solo avance, la biblioteca de cursores satisface las necesidades de muchas aplicaciones. Además, puede proporcionar un buen rendimiento, especialmente para conjuntos de resultados de tamaño pequeño a mediano, y para aplicaciones que no tienen una buena compatibilidad con cursores.  
  
 La biblioteca de cursores es una biblioteca de vínculos dinámicos (DLL) que reside entre el Administrador de controladores y el controlador. Cuando una aplicación llama a una función, el Administrador de controladores llama a la función en la biblioteca de cursores, que ejecuta la función o la llama en el controlador especificado. Para una conexión determinada, una aplicación especifica si la biblioteca de cursores siempre se utiliza, se utiliza si el controlador no admite cursores desplazables o nunca se utiliza.  
  
 La biblioteca de cursores aparece como un controlador para el Administrador de controladores. Si la biblioteca de cursores reside entre el Administrador de controladores y un controlador ODBC *2.x,* la biblioteca de cursores aparece como un controlador ODBC *2.x.* Si la biblioteca de cursores reside entre el Administrador de controladores y un controlador ODBC *3.x,* la biblioteca de cursores aparece como un controlador ODBC *3.x.* El comportamiento exhibido por la biblioteca de cursores depende de la versión del controlador con el que está trabajando, con la excepción de los desplazamientos de enlace, que se admite para los controladores ODBC *2.x* y ODBC *3.x.*  
  
 Para implementar cursores de bloque en **SQLFetch** y **SQLFetchScroll**, la biblioteca de cursores llama repetidamente **a SQLFetch** en el controlador. Para implementar el desplazamiento, almacena en caché los datos que ha recuperado en la memoria y en los archivos de disco. Cuando una aplicación solicita un nuevo conjunto de filas, la biblioteca de cursores lo recupera según sea necesario del controlador o de la memoria caché.  
  
 Para implementar instrucciones de actualización y eliminación posicionadas, la biblioteca de cursores construye una instrucción **UPDATE** o **DELETE** con una cláusula **WHERE** que especifica el valor almacenado en caché de cada columna enlazada de la fila. Cuando ejecuta una instrucción update posicionada, la biblioteca de cursores actualiza su caché a partir de los valores de los búferes del conjunto de filas.  
  
 Para obtener más información acerca de la biblioteca de cursores ODBC, consulte las secciones siguientes de este apéndice:  
  
-   [Uso de la biblioteca de cursores ODBC](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [Ejecución de instrucciones de eliminación y actualización Positioned](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [Ejemplo de código de la biblioteca de cursores](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [Notas de implementación](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [Códigos de error de la biblioteca de cursores ODBC](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)

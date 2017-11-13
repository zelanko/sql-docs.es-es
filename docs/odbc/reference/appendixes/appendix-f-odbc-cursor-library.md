---
title: "Apéndice F: biblioteca de cursores ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f48f9e35793d197efc7a72600a122abc83484ed8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="appendix-f-odbc-cursor-library"></a>Apéndice F: biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 La biblioteca de cursores ODBC (Odbccr32.dll) es compatible con los cursores desplazables de bloque para cualquier controlador que cumple con el nivel de conformidad de API de nivel 1 y puede redistribuir a los desarrolladores con sus aplicaciones o controladores. La biblioteca de cursores también admite la actualización por posición y las instrucciones delete para conjuntos de resultados generados por **seleccione** instrucciones. Aunque admite solo estáticos y solo avance, la biblioteca de cursores satisface las necesidades de muchas aplicaciones. Además, puede proporcionar un buen rendimiento, especialmente para los conjuntos de resultados de tamaño pequeño o mediano tamaño y para las aplicaciones que no tiene compatibilidad con cursores buena.  
  
 La biblioteca de cursores es una biblioteca de vínculos dinámicos (DLL) que se encuentra entre el Administrador de controladores y el controlador. Cuando una aplicación llama a una función, el Administrador de controladores llama a la función en la biblioteca de cursores, que se ejecuta la función o que lo llama en el controlador especificado. Para una conexión determinada, una aplicación especifica si la biblioteca de cursores se utiliza siempre, usa si el controlador no es compatible con los cursores desplazables o nunca se utiliza.  
  
 La biblioteca de cursores aparece como un controlador para el Administrador de controladores. Si la biblioteca de cursores que se encuentra entre el Administrador de controladores y un 2 de ODBC. *x* controlador, la biblioteca de cursores aparece como una API ODBC 2. *x* controlador. Si la biblioteca de cursores se encuentra entre el Administrador de controladores y una aplicación ODBC 3*.x* controlador, la biblioteca de cursores aparece como una aplicación ODBC 3*.x* controlador. El comportamiento que muestran la biblioteca de cursores depende de la versión del controlador se está trabajando, con la excepción de desplazamientos de enlace, que es compatible con ambos 2 de ODBC. *x* y ODBC 3. *x* controladores.  
  
 Para implementar cursores de bloque de **SQLFetch** y **SQLFetchScroll**, la biblioteca de cursores llama repetidamente **SQLFetch** en el controlador. Para implementar el desplazamiento, almacena en caché los datos que se recuperó en memoria y en archivos de disco. Cuando una aplicación solicita un nuevo conjunto de filas, la biblioteca de cursores recupera según sea necesario desde el controlador o la memoria caché.  
  
 Para implementar la actualización posicionada e instrucciones delete, la biblioteca de cursores construye una **actualizar** o **eliminar** instrucción con un **donde** cláusula que especifica las almacenadas en caché valor de cada columna enlazada en la fila. Cuando ejecuta una instrucción de actualización por posición, la biblioteca de cursores actualiza su caché de los valores de los búferes de conjunto de filas.  
  
 Para obtener más información acerca de la biblioteca de cursores ODBC, vea las siguientes secciones de este apéndice:  
  
-   [Uso de la biblioteca de cursores ODBC](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [Ejecutar instrucciones de eliminación y actualización posicionada](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [Ejemplo de código de biblioteca de cursor](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [Notas de implementación](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [Códigos de Error de biblioteca de cursores ODBC](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)


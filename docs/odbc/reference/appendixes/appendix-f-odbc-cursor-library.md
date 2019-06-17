---
title: 'Apéndice F: Biblioteca de cursores ODBC | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c27845976651b0d68b91b6269a21d1cae3518df8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267799"
---
# <a name="appendix-f-odbc-cursor-library"></a>Apéndice F: Biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 La biblioteca de cursores ODBC (Odbccr32.dll) es compatible con los cursores desplazables de bloque para cualquier controlador que cumple el nivel de conformidad de la API de nivel 1 y puede distribuirse por los desarrolladores con sus aplicaciones o controladores. La biblioteca de cursores también admite conjuntos de resultados generados por instrucciones posicionada update y delete **seleccione** instrucciones. Aunque admite cursores de solo estáticos y solo avance, la biblioteca de cursores satisface las necesidades de muchas aplicaciones. Además, puede proporcionar un buen rendimiento, especialmente para los conjuntos de resultados de tamaño pequeño o mediano tamaño y para las aplicaciones que no tienen compatibilidad con cursores buena.  
  
 La biblioteca de cursores es una biblioteca de vínculos dinámicos (DLL) que se encuentra entre el Administrador de controladores y el controlador. Cuando una aplicación llama a una función, el Administrador de controladores llama a la función en la biblioteca de cursores, que ejecuta la función o lo llama en el controlador especificado. Para una conexión determinada, una aplicación especifica si la biblioteca de cursores es siempre utiliza, usa si el controlador no es compatible con los cursores desplazables o nunca se utiliza.  
  
 La biblioteca de cursores aparece como un controlador para el Administrador de controladores. Si la biblioteca de cursores que se encuentra entre el Administrador de controladores y un 2 de ODBC. *x* controlador, la biblioteca de cursores aparece como un ODBC 2. *x* controlador. Si la biblioteca de cursores se encuentra entre el Administrador de controladores y una aplicación ODBC 3 *.x* controlador, la biblioteca de cursores aparece como una aplicación ODBC 3 *.x* controlador. El comportamiento que mostró la biblioteca de cursores depende de la versión del controlador se está trabajando, a excepción de desplazamientos de enlace, que es compatible con ambos ODBC 2. *x* y ODBC 3. *x* controladores.  
  
 Para implementar cursores de bloque en **SQLFetch** y **SQLFetchScroll**, llama repetidamente a la biblioteca de cursores **SQLFetch** en el controlador. Para implementar el desplazamiento, lo almacena en caché los datos que ha recuperado en la memoria y en los archivos de disco. Cuando una aplicación solicita un nuevo conjunto de filas, en la biblioteca de cursores se recupera según sea necesario desde el controlador o la memoria caché.  
  
 Para implementar la actualización posicionada e instrucciones delete, la biblioteca de cursores construye un **actualizar** o **eliminar** instrucción con un **donde** cláusula que especifica el almacenado en caché valor de cada columna enlazada en la fila. Cuando ejecuta una instrucción de actualización por posición, la biblioteca de cursores actualiza su caché de los valores de los búferes de conjunto de filas.  
  
 Para obtener más información acerca de la biblioteca de cursores ODBC, vea las siguientes secciones de este apéndice:  
  
-   [Uso de la biblioteca de cursores ODBC](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [Ejecución de instrucciones de eliminación y actualización Positioned](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [Ejemplo de código de la biblioteca de cursores](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [Notas de implementación](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [Códigos de error de la biblioteca de cursores ODBC](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)

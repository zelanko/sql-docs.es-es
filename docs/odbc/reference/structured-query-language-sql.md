---
title: Lenguaje de consulta estructurado (SQL) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c669b4424271fc1a3c91dea37159474fb52b97cd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293395"
---
# <a name="structured-query-language-sql"></a>Lenguaje de consulta estructurado (SQL)
Un DBMS típico permite a los usuarios almacenar, acceder y modificar datos de una manera organizada y eficiente. Originalmente, los usuarios de DBMS eran programadores. Para acceder a los datos almacenados es necesario escribir un programa en un lenguaje de programación como COBOL. Si bien estos programas se escribieron a menudo para presentar una interfaz amigable a un usuario no técnico, el acceso a los datos en sí requería los servicios de un programador experto. El acceso casual a los datos no era práctico.  
  
 Los usuarios no estaban del todo contentos con esta situación. Aunque podían acceder a los datos, a menudo requería convencer a un programador de DBMS para que escribiera software especial. Por ejemplo, si un departamento de ventas quería ver las ventas totales del mes anterior por cada uno de sus vendedores y quería que esta información se clasificara en orden por la duración del servicio de cada vendedor en la empresa, tenía dos opciones: o bien existía un programa que permitía acceder a la información exactamente de esta manera, o el departamento tenía que pedir a un programador que escribiera dicho programa. En muchos casos, esto era más trabajo de lo que valía, y siempre fue una solución costosa para consultas de una sola vez, o ad hoc. A medida que más y más usuarios querían un acceso fácil, este problema se hizo cada vez más grande.  
  
 Para permitir a los usuarios acceder a los datos de forma ad hoc, es necesario darles un idioma en el que expresar sus solicitudes. Una sola solicitud a una base de datos se define como una consulta; un lenguaje de este tipo se denomina lenguaje de consulta. Muchos lenguajes de consulta fueron desarrollados para este propósito, pero uno de ellos se convirtió en el más popular: Structured Query Language, inventado en IBM en la década de 1970. Es más comúnmente conocido por su acrónimo, SQL, y se pronuncia tanto como "ess-cue-ell" como como "secuencia". SQL se convirtió en un estándar ANSI en 1986 y un estándar ISO en 1987; se utiliza hoy en día en una gran cantidad de sistemas de gestión de bases de datos.  
  
 Aunque SQL resolvió las necesidades ad hoc de los usuarios, la necesidad de acceso a los datos por parte de los programas informáticos no desaparece. De hecho, la mayoría del acceso a la base de datos todavía era (y es) programático, en forma de informes programados regularmente y análisis estadísticos, programas de entrada de datos como los utilizados para la entrada de pedidos y programas de manipulación de datos, como los utilizados para conciliar cuentas y generar órdenes de trabajo.  
  
 Estos programas también utilizan SQL, utilizando una de las tres técnicas siguientes:  
  
-   **SQL incrustado**, en el que las instrucciones SQL se incrustan en un lenguaje host como C o COBOL.  
  
-   **Módulos SQL,** en los que las instrucciones SQL se compilan en el DBMS y se llama desde un lenguaje host.  
  
-   **Interfaz de nivel de llamada**o CLI, que consta de funciones llamadas para pasar instrucciones SQL al DBMS y recuperar los resultados del DBMS.  
  
> [!NOTE]  
>  Es un accidente histórico que se utilice el término interfaz de nivel de llamada en lugar de interfaz de programación de aplicaciones (API), otro término para la misma cosa. En el mundo de la base de datos, la API se utiliza para describir el propio SQL: SQL es la API de un DBMS.  
  
 De estas opciones, SQL incrustado es el más utilizado, aunque la mayoría de los DBMS principales admiten CLI propietarias.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Procesamiento de una instrucción SQL](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [SQL incrustado](../../odbc/reference/embedded-sql.md)  
  
-   [Módulos SQL](../../odbc/reference/sql-modules.md)  
  
-   [Interfaces de nivel de llamada](../../odbc/reference/call-level-interfaces.md)

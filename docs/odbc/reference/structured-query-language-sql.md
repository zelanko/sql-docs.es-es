---
title: Estructura de lenguaje de consulta (SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a32983b1dd4faaa64c09f5ccc773fd4ce78f3533
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909555"
---
# <a name="structured-query-language-sql"></a>Lenguaje de consulta estructurado (SQL)
Un DBMS típico permite a los usuarios almacenar, acceder y modificar los datos de manera eficiente y organizada. Originalmente, los usuarios de los DBMS eran los programadores. Obtener acceso a los datos almacenados, es necesario escribir un programa en un lenguaje de programación como COBOL. Aunque estos programas a menudo se escribieron para presentar una interfaz sencilla para un usuario no técnico, acceso a los mismos datos requiere los servicios de un programador experto. No era práctico acceso ocasional a los datos.  
  
 Los usuarios no eran completamente satisfechos con esta situación. Mientras que podrían tener acceso a datos, a menudo necesario convencer a un programador DBMS para escribir software especial. Por ejemplo, si un departamento de ventas desea ver las ventas totales del mes anterior por cada uno de sus vendedores y quería esta información por orden de clasificación por la longitud de cada vendedor de servicio en la empresa, tenía dos opciones: ya sea un programa ya existía que permite la información tener acceso a tal, o el departamento tuvo que pide a un programador escribir este tipo de programa. En muchos casos, esto era más trabajo que se valió la pena y siempre era una solución costosa para consultas ad hoc, o un solo uso. Como cada vez más usuarios deseaban de fácil acceso, este problema ha crecido más grandes y más grandes.  
  
 Permitir a los usuarios tener acceso a datos en forma ad-hoc requiere concederles un idioma en que se va a expresar sus solicitudes. Una única solicitud para una base de datos se define como una consulta; Este tipo de lenguaje se denomina un lenguaje de consulta. Muchos lenguajes de consulta se desarrollaron para este propósito, pero uno de ellos se convirtió en los más populares: lenguaje de consulta estructurado, inventado en IBM en la década de 1970. Es más conocido por su sigla, SQL y se pronuncia tanto como "See-cue ell" como "continuación". SQL se convirtió en un estándar en 1986 ANSI y una imagen ISO estándar en 1987; se usa hoy en día en un excelente muchos sistemas de administración de base de datos.  
  
 Aunque SQL resolver las necesidades ad hoc de los usuarios, la necesidad de acceso a los datos por los programas informáticos no desapareció. De hecho, la mayoría de base de datos acceso todavía era (y es) programas de entrada de datos mediante programación, en forma de conexión programados periódicamente informes y análisis estadísticos, como los utilizados para entrada de pedidos y datos de programas de manipulación, como los utilizados para conciliar las cuentas y generar pedidos de trabajo.  
  
 Estos programas también usan SQL, con una de las tres técnicas siguientes:  
  
-   **SQL incrustadas**, en qué SQL instrucciones se incrustan en un lenguaje de host como C o COBOL.  
  
-   **Los módulos SQL**, en las instrucciones SQL que se compilan en el DBMS y se llama desde un lenguaje de host.  
  
-   **Interfaz de nivel de llamada**, o la CLI, que consta de las funciones de llamada para pasar instrucciones SQL para el DBMS y recuperar resultados de la instancia de DBMS.  
  
> [!NOTE]  
>  Es un accidente histórico que el término se utiliza la interfaz de nivel de llamada en lugar de programación de aplicaciones (API), la interfaz otro término para lo mismo. En el mundo de la base de datos, API se usa para describir el mismo SQL: SQL es la API de un DBMS.  
  
 De estas opciones, SQL incrustado es el más comúnmente utilizado, aunque la mayoría de los DBMS principales admite CLI propietarias.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Procesar una instrucción SQL](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [SQL incrustado](../../odbc/reference/embedded-sql.md)  
  
-   [Módulos SQL](../../odbc/reference/sql-modules.md)  
  
-   [Interfaces de nivel de llamada](../../odbc/reference/call-level-interfaces.md)

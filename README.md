# Tipos de parâmetros

`src>index.js :`

    const express = require('express');

    const app = express();

    /**
    ** GET - Buscar uma informação dentro do servidor 
    ** POST - Inserir uma informação no servidor
    ** PUT - Alterar uma informação no servidor
    ** PATCH - Alterar uma informação específica
    ** DELETE - Deletar uma informação no servidor
    */

    /**
    *? Tipos de parâmetros
    * 
    ** Route Params => Identificar um recurso editar/deletar/buscar
    ** Query Params => Paginação / Filtro
    ** Body Params => Os objetos inserção/alteração (JSON)
    ** 
    */

    //* Query Params
    // {{ _.baseURL }}/courses?page=1&order=desc
    app.get("/courses", (request, response) => {
        const query = request.query;
        console.log(query) //{ page: '1', order: 'desc' }
        return response.json(["Curso 1","Curso 2","Curso 3"]);
    });

    //* Body Params
    // {{ _.baseURL }}/courses
    // {"name":"Feh","age":"19"}
    app.post("/courses", express.json(), (request, response) => {
        const body = request.body;
        console.log(body); //{ name: 'Feh', age: '19' }
        return response.json(["Curso 1","Curso 2","Curso 3","Curso 4"]);
    });

    //* Route Params
    // {{ _.baseURL }}/courses/1
    app.put("/courses/:id", (request,response) => {
        // const params = request.params;
        // console.log(params) // { id: '1' }
        const {id} = request.params;
        console.log(id) // 1
        return response.json(["Curso 6","Curso 2","Curso 3","Curso 4"]);
    })

    app.patch("/courses/:id", (request,response) => {
        return response.json(["Curso 6","Curso 7","Curso 3","Curso 4"]);
    })

    app.delete("/courses/:id", (request,response) => {
        return response.json(["Curso 6","Curso 2","Curso 4"]);
    })

    app.listen(3333);
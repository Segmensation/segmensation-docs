Adding new functionality
========================

Due to the underlying Client-Server-Architecture, the functionality 
of Segmensation is easily expandable. The process consists of three steps: 

- Including new interfaces in the frontend
- Adding new python scripts to the backend
- Handling response data

The communication between frontend and backend is realized through HTTP 
requests.

Adding frontend interfaces
--------------------------

.. warning:: 
    This part has to be done inside the 
    `segmensation-app <https://github.com/Segmensation/segmensation-api>`_ 
    repository.

The files in which the GUI for backend scripts are defined can be found at 
``src/scripts/``. You can either edit one of the existing comp.vue files or 
add a new one.

The interface should contain a button that starts the calculation.

.. code-block:: html

    <template>
        <v-btn :loading = "loadingBtnYourFunction" @click="btnFunction()">
            Calculate
        </v-btn>
    </template>

This button should have a corresponding function that should look similar to this:

.. code-block:: typescript

    <script lang="ts">
        // ...
        data: () => ({
            // ...
            loadingBtnYourFunction: false,
            yourParameter: ...
            // ...
        }),
        methods: {
            async btnFunction() {
                store.commit('hideModalText');
                store.commit('showModalLoading', 'Calculation of <your function> has started.');
                this.loadingBtnYourFunction = true
                try {
                    await api.yourFunction(
                        this.$store.state.selectedImageId, 
                        Math.trunc(this.selectedChannel), 
                        Math.trunc(this.selectedSliceNr), 
                        yourParameter
                    );
                    this.loadingBtnYourFunction = false;
                    store.commit('hideModalLoading');
                    store.commit('showModalText', 'Calculation of <your function> has finished.');
                } catch (error) {
                    this.loadingBtnYourFunction = false;
                    store.commit('hideModalLoading');
                    store.commit('showModalText', 'Error during caculation.');
                } 
            }
        }

Additional data is hinted at with "yourParameter" in the code above. The values 
of such Parameters can be set therough other interface elements.

When the interface is implemented, a corresponding function in the file 
``src/api/api.ts`` has to be added. This function will create and send a 
HTTP request to the backend and can pass back response data to the interface, 
e.g. to create a download option.

The function should look similar to this:

.. code-block:: typescript

    yourFunction: async (fileName: string, channel: number, slice: number, yourParameter: ...) =>
        instance.post(`/image/${fileName}/your_request`, {channel, slice, yourParameter})


Adding python scripts
---------------------

.. warning:: 
    This part has to be done inside the 
    `segmensation-api <https://github.com/Segmensation/segmensation-api>`_ 
    repository. Make sure you follow the instructions at 
    :doc:`Setting up Segmensation for development </development/setup>`.

Incoming POST requests are handled at the file app.py. Here you need to 
define a function that accepts the request, calls all needed Python 
functions and returns either resulting data or a HTTP OK response.

.. code-block:: python

    @app.post('/image/<key>/your_request')
        def your_request(key):
            # ...

These lines determine which HTTP request should be handled and define the 
function that will be called when the app receives this kind of request.

The image that should be processed can be accessed by the following function:

.. code-block:: python

    file, channel, _ = load_request_image(key)

If data from the frontend - usually user input - is needed, this data can 
be accessed by the following lines:

.. code-block:: python

    parameter = request.json[
            'yourParameter'] if request.data and 'yourParameter' in request.json else None

The 'yourParameter' is set in the frontend when the HTTP request is created.

Other contents of the function are dependent on the functionality that is 
implemented. 

If the response to the request does not contain data, the following return 
statement should be used:

.. code-block:: python

    return Response(status=200)

Otherwise you can bundle your response data into a python dictionary and convert 
it to JSON:

.. code-block:: python

    return jsonify(data)

The complete function could look similar to this:

.. code-block:: python

    @app.post('/image/<key>/calculate_orientation_jpgpng')
    def calculate_orientation_jpgpng(key):
        file, channel, _ = load_request_image(key)

        parameter = request.json[
            'parameterName'] if request.data and 'parameterName' in request.json else None

        data = yourModule.yourFunction(file, channel, parameter)
  
        return jsonify(data)


Handling response data
----------------------
.. warning:: 
    This part has to be done inside the 
    `segmensation-app <https://github.com/Segmensation/segmensation-api>`_ 
    repository.

If response data exists, it can be put into a variable by modifying the 
api call in the comp.vue from `Adding frontend interfaces`_ like this:

.. code:: typescript

    this.responseData = (
        await api.yourFunction(
            this.$store.state.selectedImageId, 
            Math.trunc(this.selectedChannel), 
            Math.trunc(this.selectedSliceNr), 
            yourParameter
        )
    ).data;

If a download button should be created, a boolean (dataCreated) can be 
introduced that signifies if response data exists. Based on this, a button 
connected to a download link can be shown:

.. code:: html

    <v-btn :style="{visibility: dataCreated ? 'visible' : 'hidden'}" @click="downloadData()">
        Download Data
    </v-btn>

The function for downloading data can look similar to this:

.. code:: typescript

    downloadData() {
      const link = document.createElement('a')
      link.href = window.URL.createObjectURL(new Blob(this.responseData, {type: "text/csv"}));
      link.download = `data.csv`
      link.click()
      URL.revokeObjectURL(link.href)
    },
# How to run Vizro-AI

This guide offers insights into different options of running Vizro-AI, including Jupyter notebook, Python scripts, and integration into your applications.

### 1. Jupyter Notebook
To run Vizro-AI in jupyter, create a new cell and execute the code below to render the described visualization. You should see the chart as an output.

??? note "Note: API key"
    Make sure you have followed the [environment setup guide](../user_guides/api_setup.md) and
    your api key is set up in a `.env` file in the same folder as your `ipynb` file.

!!! example "Bar chart"
    === "Code for the cell"
        ```py
        import vizro.plotly.express as px
        from vizro_ai import VizroAI

        from dotenv import load_dotenv
        load_dotenv()

        vizro_ai = VizroAI()

        df = px.data.gapminder()
        vizro_ai.plot(df, "visualize the life expectancy per continent and color each continent")
        ```
    === "Result"
        [![BarChart]][BarChart]

    [BarChart]: ../../assets/user_guides/bar_chart_gdp_per_continent.png

Please note that the chart's appearance may not precisely resemble the one displayed below, as it is generated by a generative AI and can vary.

### 2. Python script
You can utilize Vizro-AI in any standard development environment by creating a `.py` file and executing the following code. As a result, the rendered chart will display in a browser window.

??? note "Note: API key"
    Make sure you have followed [environment setup guide](../user_guides/api_setup.md) and
    your API key is set up in the environment where your `.py` script is running with command as below:
    ```
    export OPENAI_API_KEY="your api key"
    ```

!!! example "Line chart"
    === "example.py"
        ```py
        import vizro.plotly.express as px
        from vizro_ai import VizroAI

        vizro_ai = VizroAI()

        df = px.data.gapminder()
        vizro_ai.plot(df, "describe life expectancy per continent over time")
        ```
    === "Result"
        [![LineChart]][LineChart]

    [LineChart]: ../../assets/user_guides/line_chart_life_expect.png

### 3. Application integration

You have the possibility to integrate Vizro-AI into your application. For example, this can be achieved through a frontend that allows users to input prompts using a text field.

Vizro-AI's `_get_chart_code` method returns the Python code string that can be used to prepare the data and create the visualization. This code is validated and debugged to ensure that it is executable and ready to be integrated.

!!! example "Application integration"
    === "app.py"
        ```py
        import vizro.plotly.express as px
        from vizro_ai import VizroAI

        vizro_ai = VizroAI()

        df = px.data.gapminder()
        code_string = vizro_ai._get_chart_code(df, "describe life expectancy per continent over time", explain=True)
        ```
    === "code_string"
        [![ResultCode]][ResultCode]

    [ResultCode]: ../../assets/user_guides/code_string_app_integration.png

The returned `code_string` can be used to dynamically render charts within your application. You may have the option to encapsulate the chart within a `fig` object or convert the figure into a JSON string for further integration.

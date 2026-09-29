pipeline {
	agent any

	environment {
		PYTHON = 'C:\\Users\\hamsa\\anaconda3\\python.exe'
	}

	stages {
		stage('Install Dependencies') {
			steps {
				bat 'if not exist "%PYTHON%" (echo Python executable not found: %PYTHON% & exit /b 1)'
				bat '"%PYTHON%" --version'
				bat '"%PYTHON%" -m pip install -r requirements.txt'
			}
		}

		stage('Run Tests') {
			steps {
				bat '"%PYTHON%" -m pytest -q'
			}
		}

		stage('Build') {
			steps {
				bat '"%PYTHON%" -m py_compile app.py'
			}
		}

		stage('Deploy') {
			steps {
				bat 'if not exist deploy mkdir deploy'
				bat 'copy /Y app.py deploy\\app.py'
				bat 'copy /Y requirements.txt deploy\\requirements.txt'
				echo 'Deployment Successful'
			}
		}
	}
}
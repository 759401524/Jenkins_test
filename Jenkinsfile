pipeline {
    agent any
    stages {
        stage('Check Updates') {
            steps {
                sh '''
cd linux
git submodule update --init --recursive --depth 5 --remote
ls -alh
#curl -s https://raw.githubusercontent.com/Hexxeh/rpi-firmware/master/git_hash -o latest_version
                '''
            }
        }
        stage('Build RPI Zero') {
            environment {
                KERNEL = 'kernel'
            }
            steps {
                sh '''
rm -rf rpi_0
mkdir rpi_0 && cd rpi_0
make -f ../linux/Makefile ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcmrpi_defconfig -j4
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs -j4
'''
            }
        }
        stage('Build RPI 3') {
            environment {
                KERNEL = 'kernel7'
            }
            steps {
                sh '''
rm -rf rpi_3
mkdir rpi_3 && cd rpi_3
make -f ../linux/Makefile ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2709_defconfig -j4
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs -j4
'''
            }
        }
        stage('Build RPI 4') {
            environment {
                KERNEL = 'kernel7l'
            }
            steps {
                sh '''
rm -rf rpi_4
mkdir rpi_4 && cd rpi_4
make -f ../linux/Makefile ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bcm2711_defconfig -j4
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- zImage modules dtbs -j4
'''
            }
        }
    }
}

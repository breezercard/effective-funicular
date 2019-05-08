#include "mainwindow.h"
#include <QApplication>

QString value{""}, total{""};
int firstValue, secondValue;
bool addState{false}, minusState{false}, multiplyState{false}, divisionState{false};

MainWindow::MainWindow(QWidget *parent) :
    QMainWindow(parent)
{
    this->setWindowTitle("Basic Calculator");
    this->setStyleSheet("background-color: teal");
    label = new QLabel("0", this);
    label->setGeometry(QRect(QPoint(50,75), QSize(50,200)));
    label->setFixedSize(200,50);
    label->setAlignment(Qt::AlignRight | Qt::AlignBottom);
    label->setStyleSheet("background-color: white");
    QFont font = label->font();
    font.setPointSize(18);
    font.setBold(true);
    label->setFont(font);

    for(int i{0}; i < 6; ++i)
    {
        QString operation[] = {"C","=","+","-","x","÷"};
        operationButton[i] = new QPushButton(operation[i], this);
        if(i == 1)
        {
            connect(operationButton[i], SIGNAL(released()), this, SLOT(totalCalc()));
        }
        else
        {
            connect(operationButton[i], SIGNAL(released()), this, SLOT(operationSelect()));
        }
    }

    for(int i{0}; i < 10; ++i)
    {
        QString digit = QString::number(i);
        numberButton[i] = new QPushButton(digit, this);
        connect(numberButton[i], SIGNAL(released()), this, SLOT(digitSelect()));
    }

    setGrid();
}

void MainWindow::digitSelect()
{
    QPushButton *button = (QPushButton*)sender();
    emit numberDisplay(button->text()[0].digitValue());
    value += QString::number(button->text()[0].digitValue());
    label->setText(value);
}

void MainWindow::operationSelect()
{
    QPushButton *button = (QPushButton*)sender();
    firstValue = value.toInt();

    if(button->text()== "C")
    {
        value = "";
        firstValue = 0;
        secondValue = 0;
    }
    else if(button->text()== "+")
    {
        addState = true;
    }
    else if(button->text()== "-")
    {
        minusState = true;
    }
    else if(button->text()== "x")
    {
        multiplyState = true;
    }
    else if(button->text()== "÷")
    {
        divisionState = true;
    }

    value = "";
    label->setText(value);
}

void MainWindow::setGrid()
{
    for(int i {0}; i < 1; ++i)
    {
        numberButton[i]->setGeometry(QRect(QPoint(50,300), QSize(50,50)));
        operationButton[i]->setGeometry(QRect(QPoint(100,300), QSize(50,50)));
        operationButton[i + 1]->setGeometry(QRect(QPoint(150,300), QSize(50,50)));
        operationButton[i + 2]->setGeometry(QRect(QPoint(200,300), QSize(50,50)));
    }
    for(int i {1}; i < 4; ++i)
    {
        numberButton[i]->setGeometry(QRect(QPoint(50 * i,250), QSize(50,50)));
        if(i == 3)
        {
            operationButton[i]->setGeometry(QRect(QPoint(200,250), QSize(50,50)));
        }
    }
    for(int i {4}; i < 7; ++i)
    {
        numberButton[i]->setGeometry(QRect(QPoint(50 * (i - 3),200), QSize(50,50)));
        if(i == 4)
        {
            operationButton[i]->setGeometry(QRect(QPoint(200,200), QSize(50,50)));
        }
    }
    for(int i {7}; i < 10; ++i)
    {
        numberButton[i]->setGeometry(QRect(QPoint(50 * (i - 6),150), QSize(50,50)));
        if(i == 7)
        {
            operationButton[i - 2]->setGeometry(QRect(QPoint(200,150), QSize(50,50)));
        }
    }
}

void MainWindow::totalCalc()
{
    secondValue = value.toInt();
    if(addState)
    {
        total = QString::number(firstValue + secondValue);
        label->setText(total);
        addState = false;
    }
    else if(minusState)
    {
        total = QString::number(firstValue - secondValue);
        label->setText(total);
         minusState = false;
    }
    else if(multiplyState)
    {
        total = QString::number(firstValue * secondValue);
        label->setText(total);
        multiplyState = false;
    }
    else if(divisionState)
    {
        total = QString::number(firstValue / secondValue);
        label->setText(total);
        divisionState = false;
    }

    firstValue = 0;
    secondValue = 0;
    value = "";
    total = "";
}

MainWindow::~MainWindow()
{

}

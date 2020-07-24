#include <windows.h>
#include <GL/glut.h>
#include <stdlib.h>
#include <math.h>
#define M_PI 3.14

void init(void);
void tampil(void);
void mouse(int button, int state, int x, int y);
void ukuran(int,int);
void mouseMotion(int x,int y);
void keyboard(unsigned char, int, int);

float xrot = 0.0f;
float yrot = 0.0f;
float xdiff = 0.0f;
float ydiff = 0.0f;
bool mousedown = false;
int is_depth;

float xpos = 0.0f;
float ypos = 0.0f;
float zpos = 0.0f;

GLUquadricObj *qobj;

const double PI = 3.141592653589793;
int i;

void yak()
{
    glLoadIdentity();
    glTranslatef(xpos, ypos, zpos);
	 gluLookAt(0.0f, 0.0f, 30.0f, 0.0f, 0.0f, 0.0f, 0.0f, 1.0f, 0.0f);
    glRotatef(xrot, 1.0f,0.0f, 0.0f);
    glRotatef(yrot, 0.0f, 1.0f, 0.0f);
}

int main (int argc, char **argv)
{
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
	glutInitWindowSize(1000,720);
	glutInitWindowPosition(80,50);
	glutCreateWindow("TR GRAFKOM 2020");
	init();

	glutDisplayFunc(tampil);
	glutReshapeFunc(ukuran);

	glutMouseFunc(mouse);
	glutMotionFunc(mouseMotion);
	glutKeyboardFunc(keyboard);

	glutIdleFunc(tampil);
	glutMainLoop();
	return 0;
}

void init(void)
{
	glClearColor(0.0,0.0,0.0,0.0);
	glMatrixMode(GL_PROJECTION);
   // glEnable(GL_LIGHTING);
    glEnable(GL_COLOR_MATERIAL);
    glEnable(GL_LIGHT0);
    glEnable(GL_DEPTH_TEST);
    is_depth=1;
    glMatrixMode(GL_MODELVIEW);
    glPointSize(2.0);
    glLineWidth(2.0);
}

void atap()
{
	//atap depan
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 148.0/255., 132.0/255.);
	glVertex3f(-210.0,200.0,-80.0);
	glVertex3f(-410.0,500.0,-205.0);
	glVertex3f(-300.0,600.0,-225.0);
	glVertex3f(300.0,600.0,-225.0);
	glVertex3f(410.0,500.0,-205.0);
	glVertex3f(210.0,200.0,-80.0);
	glEnd();
	//atap blkng
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 148.0/255., 132.0/255.);
	glVertex3f(-410.0,200.0,-325.0);
	glVertex3f(-300.0,600.0,-225.0);
	glVertex3f(300.0,600.0,-225.0);
	glVertex3f(410.0,200.0,-325.0);
	glEnd();
	//atap depan tembok kiri
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 148.0/255., 132.0/255.);
	glVertex3f(-210.0,200.0,-80.0);
	glVertex3f(-410.0,500.0,-205.0);
	glVertex3f(-1000.0,500.0,-30.0);
	glVertex3f(-750.0,200.0,10.0);
	glEnd();
	//atap belakang tembok kiri
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 148.0/255., 132.0/255.);
	glVertex3f(-410.0,200.0,-300.0);
	glVertex3f(-410.0,500.0,-205.0);
	glVertex3f(-1000.0,500.0,-30.0);
	glVertex3f(-1200.0,200.0,-10.0);
	glEnd();

	glBegin(GL_TRIANGLES);
	glColor3f (165.0/255.0, 148.0/255., 132.0/255.);
	glVertex3f(-1200.0,200.0,-10.0);
	glVertex3f(-1000.0,500.0,-30.0);
	glVertex3f(-750.0,200.0,10.0);
	glEnd();

	//atap depan tembok kanan
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 148.0/255., 132.0/255.);
	glVertex3f(210.0,200.0,-80.0);
	glVertex3f(410.0,500.0,-205.0);
	glVertex3f(1000.0,500.0,-30.0);
	glVertex3f(750.0,200.0,10.0);
	glEnd();
	//atap belakang tembok kanan
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 148.0/255., 132.0/255.);
	glVertex3f(410.0,200.0,-300.0);
	glVertex3f(410.0,500.0,-205.0);
	glVertex3f(1000.0,500.0,-30.0);
	glVertex3f(1200.0,200.0,-10.0);
	glEnd();

	glBegin(GL_TRIANGLES);
	glColor3f (165.0/255.0, 148.0/255., 132.0/255.);
	glVertex3f(1200.0,200.0,-10.0);
	glVertex3f(1000.0,500.0,-30.0);
	glVertex3f(750.0,200.0,10.0);
	glEnd();

	glLineWidth(7);
	glBegin(GL_LINES);
	glColor3f(1,1,1);
	//miring kiri tengah
	glVertex3f(-410.0,500.0,-205.0);
	glVertex3f(-210.0,200.0,-80.0);
	//miring kiri
	glVertex3f(-1000.0,500.0,-30.0);
	glVertex3f(-750.0,200.0,10.0);
	//miring kiri pol
	glVertex3f(-1200.0,200.0,-10.0);
	glVertex3f(-1000.0,500.0,-30.0);

	//miring kanan tengah
	glVertex3f(410.0,500.0,-205.0);
	glVertex3f(210.0,200.0,-80.0);
	//miring kanan
	glVertex3f(1000.0,500.0,-30.0);
	glVertex3f(750.0,200.0,10.0);
	//miring kanan pol
	glVertex3f(1200.0,200.0,-10.0);
	glVertex3f(1000.0,500.0,-30.0);

	//atas dari kiri ke kanan :v
	glVertex3f(-1000.0,500.0,-30.0);
	glVertex3f(-410.0,500.0,-205.0);

	glVertex3f(-410.0,500.0,-205.0);
	glVertex3f(-300.0,600.0,-225.0);

	glVertex3f(-300.0,600.0,-225.0);
	glVertex3f(300.0,600.0,-225.0);

	glVertex3f(410.0,500.0,-205.0);
	glVertex3f(300.0,600.0,-225.0);

	glVertex3f(1000.0,500.0,-30.0);
	glVertex3f(410.0,500.0,-205.0);
	glEnd();

}
void atas()
{
	//atas
	glBegin(GL_QUADS);//ungu tengah kiri
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(-210.0,210.0,-60.0);
	glVertex3f(-70.0,210.0,-60.0);
	glVertex3f(-70.0,200.0,-60.0);
	glVertex3f(-210.0,200.0,-60.0);
	glEnd();
	glBegin(GL_QUADS);//ungu tengah kanan
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(210.0,210.0,-60.0);
	glVertex3f(70.0,210.0,-60.0);
	glVertex3f(70.0,200.0,-60.0);
	glVertex3f(210.0,200.0,-60.0);
	glEnd();
	glBegin(GL_QUADS);//putih tengah
	glColor3f (1.0,1.0,1.0);
	glVertex3f(-210.0,200.0,-100.0);
	glVertex3f(210.0,200.0,-100.0);
	glVertex3f(210.0,200.0,-60.0);
	glVertex3f(-210.0,200.0,-60.0);
	glEnd();
	glBegin(GL_POLYGON);//putih kiri
	glColor3f (1.0,1.0,1.0);
	glVertex3f(-210.0,200.0,-60.0);
	glVertex3f(-210.0,200.0,-100.0);
	glVertex3f(-750.0,200.0,0.0);
	glVertex3f(-750.0,200.0,20.0);
	glEnd();
	glBegin(GL_QUADS);//ungu kiri
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(-590.0,210.0,-4.0);
	glVertex3f(-590.0,200.0,-4.0);
	glVertex3f(-750.0,200.0,20.0);
	glVertex3f(-750.0,210.0,20.0);
	glEnd();
	glBegin(GL_QUADS);//ungu kiri
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(-210.0,210.0,-60.0);
	glVertex3f(-210.0,200.0,-60.0);
	glVertex3f(-430.0,200.0,-28.0);
	glVertex3f(-430.0,210.0,-28.0);
	glEnd();

	//kiri
	glBegin(GL_POLYGON);//putihpolkiri==============================
	glColor3f (1.0,1.0,1.0);
	glVertex3f(-750.0,200.0,0.0);
	glVertex3f(-750.0,200.0,20.0);
	glVertex3f(-1200.0,200.0,0.0);
	glVertex3f(-1200.0,200.0,-10.0);
	glEnd();
	glBegin(GL_QUADS);//ungupolkiri
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(-750.0,210.0,20.0);
	glVertex3f(-750.0,200.0,20.0);
	glVertex3f(-1200.0,200.0,0.0);
	glVertex3f(-1200.0,210.0,0.0);
	glEnd();

	glBegin(GL_POLYGON);//putih kanan
	glColor3f (1.0,1.0,1.0);
	glVertex3f(210.0,200.0,-60.0);
	glVertex3f(210.0,200.0,-100.0);
	glVertex3f(750.0,200.0,0.0);
	glVertex3f(750.0,200.0,20.0);
	glEnd();
	glBegin(GL_QUADS);//ungu kanan
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(590.0,210.0,-4.0);
	glVertex3f(590.0,200.0,-4.0);
	glVertex3f(750.0,200.0,20.0);
	glVertex3f(750.0,210.0,20.0);
	glEnd();
	glBegin(GL_QUADS);//ungu kiri
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(210.0,210.0,-60.0);
	glVertex3f(210.0,200.0,-60.0);
	glVertex3f(430.0,200.0,-28.0);
	glVertex3f(430.0,210.0,-28.0);
	glEnd();

	glBegin(GL_POLYGON);//putihpolkanan===========================
	glColor3f (1.0,1.0,1.0);
	glVertex3f(750.0,200.0,0.0);
	glVertex3f(750.0,200.0,20.0);
	glVertex3f(1200.0,200.0,0.0);
	glVertex3f(1200.0,200.0,-10.0);
	glEnd();
	glBegin(GL_QUADS);//ungupolkanan
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(750.0,210.0,20.0);
	glVertex3f(750.0,200.0,20.0);
	glVertex3f(1200.0,200.0,0.0);
	glVertex3f(1200.0,210.0,0.0);
	glEnd();

	//atas tengah
	glBegin(GL_QUADS);
	glColor3f (1,1,1);
	glVertex3f(-75.0,250.0,-55.0);
	glVertex3f(-75.0,250.0,-100.0);
	glVertex3f(75.0,250.0,-100.0);
	glVertex3f(75.0,250.0,-55.0);
	glEnd();
	//atas tengah
	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(-75.0,250.0,-100.0);
	glVertex3f(-75.0,260.0,-100.0);
	glVertex3f(-75.0,260.0,-55.0);
	glVertex3f(-75.0,250.0,-55.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(-75.0,260.0,-55.0);
	glVertex3f(-75.0,250.0,-55.0);
	glVertex3f(75.0,250.0,-55.0);
	glVertex3f(75.0,260.0,-55.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(75.0,250.0,-100.0);
	glVertex3f(75.0,260.0,-100.0);
	glVertex3f(75.0,260.0,-55.0);
	glVertex3f(75.0,250.0,-55.0);
	glEnd();



}
void temboktgh()
{
	//lapis
	glBegin(GL_POLYGON);
	glColor3f (201.0/255.0, 165.0/255.0, 139.0/255.0);
	glVertex3f(-198.0,-100.0,-99.8);
	glVertex3f(-198.0,190.0,-99.8);
	glVertex3f(-85.0,190.0,-99.8);
	glVertex3f(-85.0,-100.0,-99.8);
	glEnd();

	//tengah kiri
	glBegin(GL_POLYGON);
	glColor3f (191.0/255.0, 93.0/255.0, 36.0/255.0);
	glVertex3f(-210.0,-100.0,-100.0);
	glVertex3f(-210.0,200.0,-100.0);
	glVertex3f(-70.0,200.0,-100.0);
	glVertex3f(-70.0,-100.0,-100.0);
	glEnd();

	//tengah
	glBegin(GL_POLYGON);
	glColor3f (201.0/255.0, 165.0/255.0, 139.0/255.0);
	glVertex3f(-70.0,-100.0,-60.0);
	glVertex3f(-70.0,250.0,-60.0);
	glVertex3f(70.0,250.0,-60.0);
	glVertex3f(70.0,-100.0,-60.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f (184.0/255.0, 147.0/255.0, 120.0/255.0);
	glVertex3f(-70.0,-100.0,-60.0);
	glVertex3f(-70.0,250.0,-60.0);
	glVertex3f(-70.0,250.0,-100.0);
	glVertex3f(-70.0,-100.0,-100.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f (184.0/255.0, 147.0/255.0, 120.0/255.0);
	glVertex3f(70.0,-100.0,-60.0);
	glVertex3f(70.0,250.0,-60.0);
	glVertex3f(70.0,250.0,-100.0);
	glVertex3f(70.0,-100.0,-100.0);
	glEnd();

	//lapis
	glBegin(GL_POLYGON);
	glColor3f (201.0/255.0, 165.0/255.0, 139.0/255.0);
	glVertex3f(198.0,-100.0,-99.8);
	glVertex3f(198.0,190.0,-99.8);
	glVertex3f(85.0,190.0,-99.8);
	glVertex3f(85.0,-100.0,-99.8);
	glEnd();

	//tengah kanan
	glBegin(GL_POLYGON);
	glColor3f (191.0/255.0, 93.0/255.0, 36.0/255.0);
	glVertex3f(210.0,-100.0,-100.0);
	glVertex3f(210.0,200.0,-100.0);
	glVertex3f(70.0,200.0,-100.0);
	glVertex3f(70.0,-100.0,-100.0);
	glEnd();

}
void temboksmpgkiri()
{
	//full
	glBegin(GL_POLYGON);
	glColor3f (191.0/255.0, 93.0/255.0, 36.0/255.0);
	glVertex3f(-210.0,-100.0,-100.0);
	glVertex3f(-210.0,200.0,-100.0);
	glVertex3f(-750.0,200.0,0.0);
	glVertex3f(-750.0,-100.0,0.0);
	glEnd();

	//tengah
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 195.0/255.0, 100.0/255.0);
	glVertex3f(-430.0,-100.0,-28.0);
	glVertex3f(-430.0,250.0,-28.0);
	glVertex3f(-470.0,250.0,-20.0);
	glVertex3f(-515.0,400.0,-12.0);
	glVertex3f(-560.0,250.0,-8.0);
	glVertex3f(-590.0,250.0,0.0);
	glVertex3f(-590.0,-100.0,0.0);
	glEnd();

	//kanan
	glBegin(GL_POLYGON);
	glColor3f (0.0/255.0, 5.0/255.0, 100.0/255.0);
	glVertex3f(-430.0,-100.0,-28.0);
	glVertex3f(-430.0,250.0,-28.0);
	glVertex3f(-480.5,250.0,-55.0);
	glVertex3f(-480.5,-100.0,-55.0);
	glEnd();
	//kiri
	glBegin(GL_POLYGON);
	glColor3f (0.0/255.0, 5.0/255.0, 100.0/255.0);
	glVertex3f(-590.0,-100.0,0.0);
	glVertex3f(-590.0,250.0,0.0);
	glVertex3f(-650.0,250.0,-10.0);
	glVertex3f(-650.0,-100.0,-10.0);
	glEnd();

	//tutup atas kiri
	glBegin(GL_POLYGON);
	glColor3f (90.0/255.0, 190.0/255.0, 10.0/255.0);
	glVertex3f(-545.0,250.0,-3.0);
	glVertex3f(-585.0,250.0,5.0);
	glVertex3f(-660.0,250.0,-10.0);
	glVertex3f(-600.0,250.0,-20.0);
	glEnd();
	//tutup segitiga atas kiri
	glBegin(GL_POLYGON);
	glColor3f (90.0/255.0, 10.0/255.0, 10.0/255.0);
	glVertex3f(-545.0,250.0,-3.0);
	glVertex3f(-600.0,250.0,-20.0);
	glVertex3f(-540.0,400.0,-18.0);
	glVertex3f(-510.0,400.0,-10.5);
	glEnd();

	//tutup atas kaanan
	glBegin(GL_POLYGON);
	glColor3f (90.0/255.0, 190.0/255.0, 10.0/255.0);
	glVertex3f(-405.0,250.0,-27.0);
	glVertex3f(-450.0,250.0,-19.0);
	glVertex3f(-550.0,250.0,-30.0);
	glVertex3f(-480.5,250.0,-70.0);
	glEnd();
	//tutup segitiga atas kanan
	glBegin(GL_POLYGON);
	glColor3f (90.0/255.0, 10.0/255.0, 10.0/255.0);
	glVertex3f(-540.0,400.0,-18.0);
	glVertex3f(-510.0,400.0,-10.5);
	glVertex3f(-450.0,250.0,-19.0);
	glVertex3f(-550.0,250.0,-30.0);

	glEnd();


}
void temboksmpgkanan()
{
	//full atas
	glBegin(GL_POLYGON);
	glColor3f (191.0/255.0, 93.0/255.0, 36.0/255.0);
	glVertex3f(210.0,20.0,-100.0);
	glVertex3f(210.0,200.0,-100.0);
	glVertex3f(750.0,200.0,0.0);
	glVertex3f(750.0,20.0,0.0);
	glEnd();
	//full bawah
	glBegin(GL_POLYGON);
	glColor3f (201.0/255.0, 165.0/255.0, 139.0/255.0);
	glVertex3f(210.0,-100.0,-100.0);
	glVertex3f(210.0,20.0,-100.0);
	glVertex3f(750.0,20.0,0.0);
	glVertex3f(750.0,-100.0,0.0);
	glEnd();

	//tengah atas
	glBegin(GL_POLYGON);
	glColor3f (191.0/255.0, 93.0/255.0, 36.0/255.0);
	glVertex3f(430.0,130.0,-28.0);
	glVertex3f(430.0,250.0,-28.0);
	glVertex3f(475.6,250.0,-20.0);
	glVertex3f(520.0,400.0,-13.0);
	glVertex3f(560.0,250.0,-8.0);
	glVertex3f(590.0,250.0,0.0);
	glVertex3f(590.0,130.0,0.0);
	glEnd();

	//tengah bawah
	glBegin(GL_POLYGON);
	glColor3f (201.0/255.0, 165.0/255.0, 139.0/255.0);
	glVertex3f(430.0,130.0,-28.0);
	glVertex3f(430.0,-100.0,-28.0);
	glVertex3f(590.0,-100.0,0.0);
	glVertex3f(590.0,130.0,0.0);
	glEnd();

	//kiri
	glBegin(GL_POLYGON);
	glColor3f (210.0/255.0, 93.0/255.0, 36.0/255.0);
	glVertex3f(430.0,130.0,-28.0);
	glVertex3f(430.0,250.0,-28.0);
	glVertex3f(480.5,250.0,-55.0);
	glVertex3f(480.5,130.0,-55.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f (184.0/255.0, 147.0/255.0, 120.0/255.0);
	glVertex3f(430.0,130.0,-28.0);
	glVertex3f(430.0,-100.0,-28.0);
	glVertex3f(480.5,-100.0,-55.0);
	glVertex3f(480.5,130.0,-55.0);
	glEnd();

	//kanan
	glBegin(GL_POLYGON);
	glColor3f (210.0/255.0, 93.0/255.0, 36.0/255.0);
	glVertex3f(590.0,130.0,0.0);
	glVertex3f(590.0,250.0,0.0);
	glVertex3f(670.0,250.0,-18.0);
	glVertex3f(670.0,130.0,-18.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f (184.0/255.0, 147.0/255.0, 120.0/255.0);
	glVertex3f(590.0,130.0,0.0);
	glVertex3f(590.0,-100.0,0.0);
	glVertex3f(670.0,-100.0,-18.0);
	glVertex3f(670.0,130.0,-18.0);
	glEnd();

	//tutup atas kanan
	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(545.0,250.0,-3.0);
	glVertex3f(585.0,250.0,5.0);
	glVertex3f(690.0,250.0,-16.0);
	glVertex3f(600.0,250.0,-20.0);
	glEnd();

	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(585.0,260.0,5.0);
	glVertex3f(690.0,260.0,-16.0);
	glVertex3f(690.0,250.0,-16.0);
	glVertex3f(585.0,250.0,5.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(585.0,260.0,5.0);
	glVertex3f(545.0,260.0,-3.0);
	glVertex3f(545.0,250.0,-3.0);
	glVertex3f(585.0,250.0,5.0);
	glEnd();


	//tutup segitiga atas kanan
	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(545.0,250.0,-3.0);
	glVertex3f(600.0,250.0,-20.0);
	glVertex3f(540.0,400.0,-18.0);
	glVertex3f(510.0,400.0,-10.5);
	glEnd();

	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(510.0,410.0,-10.5);
	glVertex3f(510.0,400.0,-10.5);
	glVertex3f(545.0,250.0,-3.0);
	glVertex3f(545.0,260.0,-3.0);
	glEnd();

	//tutup segitiga atas kiri
	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(540.0,400.0,-18.0);
	glVertex3f(510.0,400.0,-10.5);
	glVertex3f(450.0,250.0,-19.0);
	glVertex3f(550.0,250.0,-30.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(510.0,410.0,-10.5);
	glVertex3f(510.0,400.0,-10.5);
	glVertex3f(450.0,250.0,-19.0);
	glVertex3f(450.0,260.0,-19.0);
	glEnd();

	//tutup atas kiri
	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(405.0,250.0,-27.0);
	glVertex3f(450.0,250.0,-19.0);
	glVertex3f(550.0,250.0,-30.0);
	glVertex3f(480.5,250.0,-70.0);
	glEnd();
	
	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(480.0,260.0,-70.0);
	glVertex3f(405.0,260.0,-27.0);
	glVertex3f(405.0,250.0,-27.0);
	glVertex3f(480.0,250.0,-70.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f (2.0/255.0, 0.0/255., 50.0/255.);
	glVertex3f(405.0,260.0,-27.0);
	glVertex3f(405.0,250.0,-27.0);
	glVertex3f(450.0,250.0,-19.0);
	glVertex3f(450.0,260.0,-19.0);
	glEnd();

	//shell tengah
	glBegin(GL_POLYGON);
	glColor3f (201.0/255.0, 165.0/255.0, 139.0/255.0);
	glVertex3f(429.8,250.0,-28.0);
	glVertex3f(590.0,250.0,0.0);
	glVertex3f(589.9,240.0,0.0);
	glVertex3f(429.8,240.0,-28.0);
	glEnd();

	//shell kanan
	glBegin(GL_POLYGON);
	glColor3f (184.0/255.0, 147.0/255.0, 120.0/255.0);
	glVertex3f(590.0,250.0,0.1);
	glVertex3f(589.9,240.0,0.1);
	glVertex3f(670.0,240.0,-17.9);
	glVertex3f(670.0,250.0,-17.9);
	glEnd();
	
	//shell kiri
	glBegin(GL_POLYGON);
	glColor3f (184.0/255.0, 147.0/255.0, 120.0/255.0);
	glVertex3f(429.8,250.0,-28.1);
	glVertex3f(429.8,240.0,-28.1);
	glVertex3f(480.5,240.0,-55.1);
	glVertex3f(480.5,250.0,-55.1);
	glEnd();

	//wajik
	glBegin(GL_POLYGON);
	glColor3f (184.0/255.0, 147.0/255.0, 120.0/255.0);
	glVertex3f(500.6,300.0,-16.0);
	glVertex3f(509.6,330.0,-15.0);
	glVertex3f(520.6,300.0,-13.5);
	glVertex3f(510.6,270.0,-15.0);
	glEnd();

}
void tembokblkng()
{

	//tengahblkng
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 95.0/255.0, 100.0/255.0);
	glVertex3f(-410.0,-100.0,-300.0);
	glVertex3f(-410.0,200.0,-300.0);
	glVertex3f(410.0,200.0,-300.0);
	glVertex3f(410.0,-100.0,-300.0);
	glEnd();

	//kiri
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 95.0/255.0, 10.0/255.0);
	glVertex3f(-750.0,-100.0,0.0);
	glVertex3f(-750.0,200.0,0.0);
	glVertex3f(-1200.0,200.0,-10.0);
	glVertex3f(-1200.0,-100.0,-10.0);
	glEnd();

	//smpgkiriblkng
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 95.0/255.0, 100.0/255.0);
	glVertex3f(-410.0,-100.0,-300.0);
	glVertex3f(-410.0,200.0,-300.0);
	glVertex3f(-1200.0,200.0,-10.0);
	glVertex3f(-1200.0,-100.0,-10.0);
	glEnd();

	//kanan atas
	glBegin(GL_POLYGON);
	glColor3f (210.0/255.0, 93.0/255.0, 36.0/255.0);
	glVertex3f(750.0,20.0,0.0);
	glVertex3f(750.0,200.0,0.0);
	glVertex3f(1200.0,200.0,-10.0);
	glVertex3f(1200.0,20.0,-10.0);
	glEnd();

	//kanan bawah
	glBegin(GL_POLYGON);
	glColor3f (184.0/255.0, 147.0/255.0, 120.0/255.0);
	glVertex3f(750.0,-100.0,0.0);
	glVertex3f(750.0,20.0,0.0);
	glVertex3f(1200.0,20.0,-10.0);
	glVertex3f(1200.0,-100.0,-10.0);
	glEnd();

	//smpgkananblkng
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 95.0/255.0, 100.0/255.0);
	glVertex3f(410.0,-100.0,-300.0);
	glVertex3f(410.0,200.0,-300.0);
	glVertex3f(1200.0,200.0,-10.0);
	glVertex3f(1200.0,-100.0,-10.0);
	glEnd();
}
void jendelapolkiri()
{
    glLineWidth(3);
	glColor3f(1.0,1.0,1.0);
	glBegin(GL_LINES);
	//bagian atas
	glVertex3f(-780.0,175.0,0.0);//jendela 1 vertikal
	glVertex3f(-780.0,110.0,0.0);
	glVertex3f(-830.0,110.0,0.0);
	glVertex3f(-830.0,175.0,0.0);
	glVertex3f(-780.0,175.0,0.0);//horizontal
	glVertex3f(-830.0,175.0,0.0);
	glVertex3f(-780.0,110.0,0.0);
	glVertex3f(-830.0,110.0,0.0);

	glVertex3f(-950.0,175.0,-4.0);//jendela 2 vertikal
	glVertex3f(-950.0,110.0,-4.0);
	glVertex3f(-1000.0,110.0,-4.0);
	glVertex3f(-1000.0,175.0,-4.0);
	glVertex3f(-950.0,175.0,-4.0);//horizontal
	glVertex3f(-1000.0,175.0,-4.0);
	glVertex3f(-1000.0,110.0,-4.0);
	glVertex3f(-950.0,110.0,-4.0);

	glVertex3f(-1170.0,175.0,-9.0);//jendela 3 vertikal
	glVertex3f(-1170.0,110.0,-9.0);
	glVertex3f(-1120.0,110.0,-8.0);
	glVertex3f(-1120.0,175.0,-8.0);
	glVertex3f(-1170.0,175.0,-9.0);//horizontal
	glVertex3f(-1120.0,175.0,-8.0);
	glVertex3f(-1120.0,110.0,-8.0);
	glVertex3f(-1170.0,110.0,-9.0);

    //bagian tengah
	glVertex3f(-850.0,85.0,-2.0);//jendela 1 vertikal
	glVertex3f(-850.0,20.0,-2.0);
	glVertex3f(-900.0,20.0,-2.1);
	glVertex3f(-900.0,85.0,-2.1);
	glVertex3f(-850.0,85.0,-2.0);//horizontal
	glVertex3f(-900.0,85.0,-2.1);
	glVertex3f(-850.0,20.0,-2.0);
	glVertex3f(-900.0,20.0,-2.1);

	glVertex3f(-930.0,85.0,-4.0);//jendela 2 vertikal
	glVertex3f(-930.0,20.0,-4.0);
	glVertex3f(-985.0,20.0,-5.0);
	glVertex3f(-985.0,85.0,-5.0);
	glVertex3f(-930.0,85.0,-4.0);//horizontal
	glVertex3f(-985.0,85.0,-5.0);
	glVertex3f(-930.0,20.0,-4.0);
	glVertex3f(-985.0,20.0,-5.0);

	glVertex3f(-985.0,85.0,-5.0);//jendela 3 vertikal
	glVertex3f(-985.0,20.0,-5.0);
	glVertex3f(-1035.0,20.0,-5.0);
	glVertex3f(-1035.0,85.0,-5.0);
	glVertex3f(-985.0,85.0,-5.0);//horizontal
	glVertex3f(-1035.0,85.0,-5.0);
	glVertex3f(-985.0,20.0,-5.0);
	glVertex3f(-1035.0,20.0,-5.0);

	glVertex3f(-1065.0,85.0,-5.5);//jendela 4 vertikal
	glVertex3f(-1065.0,20.0,-5.5);
	glVertex3f(-1115.0,20.0,-6.5);
	glVertex3f(-1115.0,85.0,-6.5);
	glVertex3f(-1065.0,85.0,-5.5);//horizontal
	glVertex3f(-1115.0,85.0,-6.5);
	glVertex3f(-1115.0,20.0,-6.5);
	glVertex3f(-1065.0,20.0,-5.5);
	//bagianbawah
	glVertex3f(-850.0,-17.0,-2.0);//jendela 1 vertikal
	glVertex3f(-850.0,-82.0,-2.0);
	glVertex3f(-900.0,-82.0,-2.1);
	glVertex3f(-900.0,-17.0,-2.1);
	glVertex3f(-850.0,-82.0,-2.0);//horizontal
	glVertex3f(-900.0,-82.0,-2.1);
	glVertex3f(-850.0,-17.0,-2.0);
	glVertex3f(-900.0,-17.0,-2.1);

	glVertex3f(-930.0,-17.0,-4.0);//jendela 2 vertikal
	glVertex3f(-930.0,-82.0,-4.0);
	glVertex3f(-985.0,-82.0,-5.0);
	glVertex3f(-985.0,-17.0,-5.0);
	glVertex3f(-930.0,-82.0,-4.0);//horizontal
	glVertex3f(-985.0,-82.0,-5.0);
	glVertex3f(-930.0,-17.0,-4.0);
	glVertex3f(-985.0,-17.0,-5.0);

	glVertex3f(-985.0,-17.0,-5.0);//jendela 3 vertikal
	glVertex3f(-985.0,-82.0,-5.0);
	glVertex3f(-1035.0,-82.0,-5.0);
	glVertex3f(-1035.0,-17.0,-5.0);
	glVertex3f(-985.0,-82.0,-5.0);//horizontal
	glVertex3f(-1035.0,-82.0,-5.0);
	glVertex3f(-985.0,-17.0,-5.0);
	glVertex3f(-1035.0,-17.0,-5.0);

	glVertex3f(-1065.0,-17.0,-5.5);//jendela 4 vertikal
	glVertex3f(-1065.0,-82.0,-5.5);
	glVertex3f(-1115.0,-82.0,-6.5);
	glVertex3f(-1115.0,-17.0,-6.5);
	glVertex3f(-1065.0,-82.0,-5.5);//horizontal
	glVertex3f(-1115.0,-82.0,-6.5);
	glVertex3f(-1115.0,-17.0,-6.5);
	glVertex3f(-1065.0,-17.0,-5.5);
	glEnd();

    glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	//atas
	glVertex3f(-780.0,175.0,0.0);//jendela 1 vertikal
	glVertex3f(-780.0,110.0,0.0);
	glVertex3f(-830.0,110.0,0.0);
	glVertex3f(-830.0,175.0,0.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-950.0,175.0,-4.0);//jendela 2 vertikal
	glVertex3f(-950.0,110.0,-4.0);
	glVertex3f(-1000.0,110.0,-4.0);
	glVertex3f(-1000.0,175.0,-4.0);
	glEnd();
    glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-1170.0,175.0,-9.0);//jendela 3 vertikal
	glVertex3f(-1170.0,110.0,-9.0);
	glVertex3f(-1120.0,110.0,-8.2);
	glVertex3f(-1120.0,175.0,-8.2);
	glEnd();
    glBegin(GL_POLYGON);//tengah
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-850.0,85.0,-2.0);//jendela 1 vertikal
	glVertex3f(-850.0,20.0,-2.0);
	glVertex3f(-900.0,20.0,-2.1);
	glVertex3f(-900.0,85.0,-2.1);
	glEnd();
    glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-930.0,85.0,-4.0);//jendela 2 vertikal
	glVertex3f(-930.0,20.0,-4.0);
	glVertex3f(-985.0,20.0,-5.1);
	glVertex3f(-985.0,85.0,-5.1);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-985.0,85.0,-5.0);//jendela 3 vertikal
	glVertex3f(-985.0,20.0,-5.0);
	glVertex3f(-1035.0,20.0,-5.0);
	glVertex3f(-1035.0,85.0,-5.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-1065.0,85.0,-5.5);//jendela 4 vertikal
	glVertex3f(-1065.0,20.0,-5.5);
	glVertex3f(-1115.0,20.0,-6.5);
	glVertex3f(-1115.0,85.0,-6.5);
	glEnd();
	glBegin(GL_POLYGON);//bawah
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-850.0,-17.0,-2.0);//jendela 1 vertikal
	glVertex3f(-850.0,-82.0,-2.0);
	glVertex3f(-900.0,-82.0,-2.0);
	glVertex3f(-900.0,-17.0,-2.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-930.0,-17.0,-4.0);//jendela 2 vertikal
	glVertex3f(-930.0,-82.0,-4.0);
	glVertex3f(-983.0,-82.0,-5.0);
	glVertex3f(-983.0,-17.0,-5.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-985.0,-82.0,-5.0);//jendela 3 vertikal
	glVertex3f(-985.0,-17.0,-5.0);
	glVertex3f(-1035.0,-17.0,-5.0);
	glVertex3f(-1035.0,-82.0,-5.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-1065.0,-82.0,-5.5);//jendela 4 vertikal
	glVertex3f(-1065.0,-17.0,-5.5);
	glVertex3f(-1115.0,-17.0,-6.5);
	glVertex3f(-1115.0,-82.0,-6.5);
	glEnd();

	glLineWidth(2);
	glColor3f(1.0,1.0,1.0);
	glBegin(GL_LINES);//1
	glVertex3f(-805.0,175.0,0.1);
	glVertex3f(-805.0,110.0,0.1);
	glVertex3f(-780.0,142.0,0.1);
	glVertex3f(-830.0,142.0,0.1);

	glVertex3f(-975.0,175.0,-3.9);//2
	glVertex3f(-975.0,110.0,-3.9);
	glVertex3f(-950.0,142.0,-3.9);
	glVertex3f(-1000.0,142.0,-3.9);

	glVertex3f(-1143.0,175.0,-7.5);//3
	glVertex3f(-1143.0,110.0,-7.5);
    glVertex3f(-1170.0,142.0,-9.0);
	glVertex3f(-1120.0,142.0,-8.0);

	glVertex3f(-875.0,85.0,-1.9);//t1
	glVertex3f(-875.0,20.0,-1.9);
	glVertex3f(-900.0,52.5,-1.9);
	glVertex3f(-850.0,52.5,-1.9);

	glVertex3f(-955.0,85.0,-4.4);//t2
	glVertex3f(-955.0,20.0,-4.4);
	glVertex3f(-930.0,52.5,-4.0);
	glVertex3f(-985.0,52.5,-4.5);

	glVertex3f(-1003.0,85.0,-4.8);//t3
	glVertex3f(-1003.0,20.0,-4.8);
	glVertex3f(-980.0,52.5,-4.2);
	glVertex3f(-1030.0,52.5,-4.7);

	glVertex3f(-1090.0,85.0,-6.0);//t4
	glVertex3f(-1090.0,20.0,-6.0);
	glVertex3f(-1065.0,52.5,-5.2);
	glVertex3f(-1115.0,52.5,-6.2);

	glVertex3f(-875.0,-82.0,-1.9);//b1
	glVertex3f(-875.0,-15.0,-1.9);
	glVertex3f(-900.0,-49.0,-1.9);
	glVertex3f(-850.0,-49.0,-1.9);

	glVertex3f(-955.0,-82.0,-4.4);//b2
	glVertex3f(-955.0,-17.0,-4.4);
	glVertex3f(-930.0,-49.0,-4.0);
	glVertex3f(-985.0,-49.0,-4.5);

	glVertex3f(-1003.0,-82.0,-4.8);//b3
	glVertex3f(-1003.0,-17.0,-4.8);
	glVertex3f(-985.0,-49.0,-4.2);
	glVertex3f(-1030.0,-49.0,-4.7);

	glVertex3f(-1090.0,-82.0,-6.0);//b4
	glVertex3f(-1090.0,-17.0,-6.0);
	glVertex3f(-1065.0,-49.0,-5.2);
	glVertex3f(-1115.0,-49.0,-6.2);
	glEnd();
}
void jendelapolkanan()
{
     glLineWidth(3);
	glColor3f(1.0,1.0,1.0);
	glBegin(GL_LINES);
	//bagian atas
	glVertex3f(780.0,175.0,0.0);//jendela 1 vertikal
	glVertex3f(780.0,110.0,0.0);
	glVertex3f(830.0,110.0,0.0);
	glVertex3f(830.0,175.0,0.0);
	glVertex3f(780.0,175.0,0.0);//horizontal
	glVertex3f(830.0,175.0,0.0);
	glVertex3f(780.0,110.0,0.0);
	glVertex3f(830.0,110.0,0.0);

	glVertex3f(950.0,175.0,-4.0);//jendela 2 vertikal
	glVertex3f(950.0,110.0,-4.0);
	glVertex3f(1000.0,110.0,-4.0);
	glVertex3f(1000.0,175.0,-4.0);
	glVertex3f(950.0,175.0,-4.0);//horizontal
	glVertex3f(1000.0,175.0,-4.0);
	glVertex3f(1000.0,110.0,-4.0);
	glVertex3f(950.0,110.0,-4.0);

	glVertex3f(1170.0,175.0,-9.0);//jendela 3 vertikal
	glVertex3f(1170.0,110.0,-9.0);
	glVertex3f(1120.0,110.0,-8.0);
	glVertex3f(1120.0,175.0,-8.0);
	glVertex3f(1170.0,175.0,-9.0);//horizontal
	glVertex3f(1120.0,175.0,-8.0);
	glVertex3f(1120.0,110.0,-8.0);
	glVertex3f(1170.0,110.0,-9.0);

    //bagian tengah
	glVertex3f(850.0,85.0,-2.0);//jendela 1 vertikal
	glVertex3f(850.0,20.0,-2.0);
	glVertex3f(900.0,20.0,-2.1);
	glVertex3f(900.0,85.0,-2.1);
	glVertex3f(850.0,85.0,-2.0);//horizontal
	glVertex3f(900.0,85.0,-2.1);
	glVertex3f(850.0,20.0,-2.0);
	glVertex3f(900.0,20.0,-2.1);

	glVertex3f(930.0,85.0,-4.0);//jendela 2 vertikal
	glVertex3f(930.0,20.0,-4.0);
	glVertex3f(985.0,20.0,-5.0);
	glVertex3f(985.0,85.0,-5.0);
	glVertex3f(930.0,85.0,-4.0);//horizontal
	glVertex3f(985.0,85.0,-5.0);
	glVertex3f(930.0,20.0,-4.0);
	glVertex3f(985.0,20.0,-5.0);

	glVertex3f(985.0,85.0,-5.0);//jendela 3 vertikal
	glVertex3f(985.0,20.0,-5.0);
	glVertex3f(1035.0,20.0,-5.0);
	glVertex3f(1035.0,85.0,-5.0);
	glVertex3f(985.0,85.0,-5.0);//horizontal
	glVertex3f(1035.0,85.0,-5.0);
	glVertex3f(985.0,20.0,-5.0);
	glVertex3f(1035.0,20.0,-5.0);

	glVertex3f(1065.0,85.0,-5.5);//jendela 4 vertikal
	glVertex3f(1065.0,20.0,-5.5);
	glVertex3f(1115.0,20.0,-6.5);
	glVertex3f(1115.0,85.0,-6.5);
	glVertex3f(1065.0,85.0,-5.5);//horizontal
	glVertex3f(1115.0,85.0,-6.5);
	glVertex3f(1115.0,20.0,-6.5);
	glVertex3f(1065.0,20.0,-5.5);
	//bagianbawah
	glVertex3f(850.0,-17.0,-2.0);//jendela 1 vertikal
	glVertex3f(850.0,-82.0,-2.0);
	glVertex3f(900.0,-82.0,-2.1);
	glVertex3f(900.0,-17.0,-2.1);
	glVertex3f(850.0,-82.0,-2.0);//horizontal
	glVertex3f(900.0,-82.0,-2.1);
	glVertex3f(850.0,-17.0,-2.0);
	glVertex3f(900.0,-17.0,-2.1);

	glVertex3f(930.0,-17.0,-4.0);//jendela 2 vertikal
	glVertex3f(930.0,-82.0,-4.0);
	glVertex3f(985.0,-82.0,-5.0);
	glVertex3f(985.0,-17.0,-5.0);
	glVertex3f(930.0,-82.0,-4.0);//horizontal
	glVertex3f(985.0,-82.0,-5.0);
	glVertex3f(930.0,-17.0,-4.0);
	glVertex3f(985.0,-17.0,-5.0);

	glVertex3f(985.0,-17.0,-5.0);//jendela 3 vertikal
	glVertex3f(985.0,-82.0,-5.0);
	glVertex3f(1035.0,-82.0,-5.0);
	glVertex3f(1035.0,-17.0,-5.0);
	glVertex3f(985.0,-82.0,-5.0);//horizontal
	glVertex3f(1035.0,-82.0,-5.0);
	glVertex3f(985.0,-17.0,-5.0);
	glVertex3f(1035.0,-17.0,-5.0);

	glVertex3f(1065.0,-17.0,-5.5);//jendela 4 vertikal
	glVertex3f(1065.0,-82.0,-5.5);
	glVertex3f(1115.0,-82.0,-6.5);
	glVertex3f(1115.0,-17.0,-6.5);
	glVertex3f(1065.0,-82.0,-5.5);//horizontal
	glVertex3f(1115.0,-82.0,-6.5);
	glVertex3f(1115.0,-17.0,-6.5);
	glVertex3f(1065.0,-17.0,-5.5);
	glEnd();

    glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	//atas
	glVertex3f(780.0,175.0,0.0);//jendela 1 vertikal
	glVertex3f(780.0,110.0,0.0);
	glVertex3f(830.0,110.0,0.0);
	glVertex3f(830.0,175.0,0.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(950.0,175.0,-4.0);//jendela 2 vertikal
	glVertex3f(950.0,110.0,-4.0);
	glVertex3f(1000.0,110.0,-4.0);
	glVertex3f(1000.0,175.0,-4.0);
	glEnd();
    glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(1170.0,175.0,-9.0);//jendela 3 vertikal
	glVertex3f(1170.0,110.0,-9.0);
	glVertex3f(1120.0,110.0,-8.2);
	glVertex3f(1120.0,175.0,-8.2);
	glEnd();
    glBegin(GL_POLYGON);//tengah
	glColor3f(0.0,0.0,0.0);
	glVertex3f(850.0,85.0,-2.0);//jendela 1 vertikal
	glVertex3f(850.0,20.0,-2.0);
	glVertex3f(900.0,20.0,-2.1);
	glVertex3f(900.0,85.0,-2.1);
	glEnd();
    glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(930.0,85.0,-4.0);//jendela 2 vertikal
	glVertex3f(930.0,20.0,-4.0);
	glVertex3f(985.0,20.0,-5.1);
	glVertex3f(985.0,85.0,-5.1);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(985.0,85.0,-5.0);//jendela 3 vertikal
	glVertex3f(985.0,20.0,-5.0);
	glVertex3f(1035.0,20.0,-5.0);
	glVertex3f(1035.0,85.0,-5.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(1065.0,85.0,-5.5);//jendela 4 vertikal
	glVertex3f(1065.0,20.0,-5.5);
	glVertex3f(1115.0,20.0,-6.5);
	glVertex3f(1115.0,85.0,-6.5);
	glEnd();
	glBegin(GL_POLYGON);//bawah
	glColor3f(0.0,0.0,0.0);
	glVertex3f(850.0,-17.0,-2.0);//jendela 1 vertikal
	glVertex3f(850.0,-82.0,-2.0);
	glVertex3f(900.0,-82.0,-2.0);
	glVertex3f(900.0,-17.0,-2.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(930.0,-17.0,-4.0);//jendela 2 vertikal
	glVertex3f(930.0,-82.0,-4.0);
	glVertex3f(983.0,-82.0,-5.0);
	glVertex3f(983.0,-17.0,-5.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(985.0,-82.0,-5.0);//jendela 3 vertikal
	glVertex3f(985.0,-17.0,-5.0);
	glVertex3f(1035.0,-17.0,-5.0);
	glVertex3f(1035.0,-82.0,-5.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(1065.0,-82.0,-5.5);//jendela 4 vertikal
	glVertex3f(1065.0,-17.0,-5.5);
	glVertex3f(1115.0,-17.0,-6.5);
	glVertex3f(1115.0,-82.0,-6.5);
	glEnd();

	glLineWidth(2);
	glColor3f(1.0,1.0,1.0);
	glBegin(GL_LINES);//1
	glVertex3f(805.0,175.0,0.1);
	glVertex3f(805.0,110.0,0.1);
	glVertex3f(780.0,142.0,0.1);
	glVertex3f(830.0,142.0,0.1);

	glVertex3f(975.0,175.0,-3.9);//2
	glVertex3f(975.0,110.0,-3.9);
	glVertex3f(950.0,142.0,-3.9);
	glVertex3f(1000.0,142.0,-3.9);

	glVertex3f(1143.0,175.0,-7.5);//3
	glVertex3f(1143.0,110.0,-7.5);
    glVertex3f(1170.0,142.0,-9.0);
	glVertex3f(1120.0,142.0,-8.0);

	glVertex3f(875.0,85.0,-1.9);//t1
	glVertex3f(875.0,20.0,-1.9);
	glVertex3f(900.0,52.5,-1.9);
	glVertex3f(850.0,52.5,-1.9);

	glVertex3f(955.0,85.0,-4.4);//t2
	glVertex3f(955.0,20.0,-4.4);
	glVertex3f(930.0,52.5,-4.0);
	glVertex3f(985.0,52.5,-4.5);

	glVertex3f(1003.0,85.0,-4.8);//t3
	glVertex3f(1003.0,20.0,-4.8);
	glVertex3f(980.0,52.5,-4.2);
	glVertex3f(1030.0,52.5,-4.7);

	glVertex3f(1090.0,85.0,-6.0);//t4
	glVertex3f(1090.0,20.0,-6.0);
	glVertex3f(1065.0,52.5,-5.2);
	glVertex3f(1115.0,52.5,-6.2);

	glVertex3f(875.0,-82.0,-1.9);//b1
	glVertex3f(875.0,-15.0,-1.9);
	glVertex3f(900.0,-49.0,-1.9);
	glVertex3f(850.0,-49.0,-1.9);

	glVertex3f(955.0,-82.0,-4.4);//b2
	glVertex3f(955.0,-17.0,-4.4);
	glVertex3f(930.0,-49.0,-4.0);
	glVertex3f(985.0,-49.0,-4.5);

	glVertex3f(1003.0,-82.0,-4.8);//b3
	glVertex3f(1003.0,-17.0,-4.8);
	glVertex3f(985.0,-49.0,-4.2);
	glVertex3f(1030.0,-49.0,-4.7);

	glVertex3f(1090.0,-82.0,-6.0);//b4
	glVertex3f(1090.0,-17.0,-6.0);
	glVertex3f(1065.0,-49.0,-5.2);
	glVertex3f(1115.0,-49.0,-6.2);
	glEnd();
}
void jendelatengah()
{
	//jendela tengah kiri---------------------------------------------
	glLineWidth(3);
	glColor3f(92.0/255.0, 65.0/255.0, 48.0/255.0);
	glBegin(GL_LINES);
	//vertical
	glVertex3f(-187.0,18.0,-99.8);
	glVertex3f(-187.0,175.0,-99.8);
	glVertex3f(-95.0,175.0,-99.8);
	glVertex3f(-95.0,18.0,-99.8);
	glVertex3f(-157.0,18.0,-99.8);
	glVertex3f(-157.0,175.0,-99.8);
	glVertex3f(-126.0,175.0,-99.8);
	glVertex3f(-126.0,18.0,-99.8);
	//horizontal
	glVertex3f(-187.0,175.0,-99.8);
	glVertex3f(-95.0,175.0,-99.8);
	glVertex3f(-187.0,120.0,-99.8);
	glVertex3f(-95.0,120.0,-99.8);
	glVertex3f(-187.0,70.0,-99.8);
	glVertex3f(-95.0,70.0,-99.8);
	glVertex3f(-187.0,18.0,-99.8);
	glVertex3f(-95.0,18.0,-99.8);
	glEnd();

	glLineWidth(1);
	glColor3f(139.0/255.0,69.0/255.0,19.0/255.0);
	glBegin(GL_LINES);
	//horizontal
	glVertex3f(-187.0,144.5,-99.8);
	glVertex3f(-95.0,144.5,-99.8);
	glVertex3f(-187.0,93.5,-99.8);
	glVertex3f(-95.0,93.5,-99.8);
	glVertex3f(-187.0,43.5,-99.8);
	glVertex3f(-95.0,43.5,-99.8);

	//vertical
	glVertex3f(-172.0,175.0,-99.8);
	glVertex3f(-172.0,18.0,-99.8);
	glVertex3f(-141.0,175.0,-99.8);
	glVertex3f(-141.0,18.0,-99.8);
	glVertex3f(-111.0,175.0,-99.8);
	glVertex3f(-111.0,18.0,-99.8);
	glEnd();

	glBegin(GL_POLYGON);
	glColor3f (1, 1, 1);
	glVertex3f(-187.0,175.0,-99.8);
	glVertex3f(-95.0,175.0,-99.8);
	glVertex3f(-95.0,18.0,-99.8);
	glVertex3f(-187.0,18.0,-99.8);
	glEnd();
	//pintu kiri --------------------------------------
	glBegin(GL_POLYGON);
	glColor3f (99.0/225.0, 112.0/225.0, 118.0/225.0);
	glVertex3f(-180.0,-100.0,-99.8);
	glVertex3f(-102.0,-100.0,-99.8);
	glVertex3f(-102.0,0.0,-99.8);
	glVertex3f(-180.0,0.0,-99.8);
	glEnd();

	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(92.0/255.0, 65.0/255.0, 48.0/255.0);
	glVertex3f(-180.0,0.0,-99.5);
	glVertex3f(-102.0,0.0,-99.5);
	glVertex3f(-180.0,0.0,-99.5);
	glVertex3f(-180.0,-100.0,-99.5);
	glVertex3f(-102.0,0.0,-99.5);
	glVertex3f(-102.0,-100.0,-99.5);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(92.0/255.0, 65.0/255.0, 48.0/255.0);
	glVertex3f(-141.0,0.0,-99.5);
	glVertex3f(-141.0,-100.0,-99.5);
	glEnd();
	glPointSize(3);
	glColor3f(92.0/255.0, 65.0/255.0, 48.0/255.0);
	glBegin(GL_POINTS);
	glVertex3f(-150.0, -50.0, -99.5);
	glVertex3f(-131.0, -50.0, -99.5);
	glEnd();

	//jendela tengah kanan---------------------------------------------
	glLineWidth(3);
	glColor3f(92.0/255.0, 65.0/255.0, 48.0/255.0);
	glBegin(GL_LINES);
	//vertical
	glVertex3f(187.0,18.0,-99.8);
	glVertex3f(187.0,175.0,-99.8);
	glVertex3f(95.0,175.0,-99.8);
	glVertex3f(95.0,18.0,-99.8);
	glVertex3f(157.0,18.0,-99.8);
	glVertex3f(157.0,175.0,-99.8);
	glVertex3f(126.0,175.0,-99.8);
	glVertex3f(126.0,18.0,-99.8);
	//horizontal
	glVertex3f(187.0,175.0,-99.8);
	glVertex3f(95.0,175.0,-99.8);
	glVertex3f(187.0,120.0,-99.8);
	glVertex3f(95.0,120.0,-99.8);
	glVertex3f(187.0,70.0,-99.8);
	glVertex3f(95.0,70.0,-99.8);
	glVertex3f(187.0,18.0,-99.8);
	glVertex3f(95.0,18.0,-99.8);
	glEnd();

	glLineWidth(1);
	glColor3f(139.0/255.0,69.0/255.0,19.0/255.0);
	glBegin(GL_LINES);
	//horizontal
	glVertex3f(187.0,144.5,-99.8);
	glVertex3f(95.0,144.5,-99.8);
	glVertex3f(187.0,93.5,-99.8);
	glVertex3f(95.0,93.5,-99.8);
	glVertex3f(187.0,43.5,-99.8);
	glVertex3f(95.0,43.5,-99.8);

	//vertical
	glVertex3f(172.0,175.0,-99.8);
	glVertex3f(172.0,18.0,-99.8);
	glVertex3f(141.0,175.0,-99.8);
	glVertex3f(141.0,18.0,-99.8);
	glVertex3f(111.0,175.0,-99.8);
	glVertex3f(111.0,18.0,-99.8);
	glEnd();

	glBegin(GL_POLYGON);
	glColor3f (1, 1, 1);
	glVertex3f(187.0,175.0,-99.8);
	glVertex3f(95.0,175.0,-99.8);
	glVertex3f(95.0,18.0,-99.8);
	glVertex3f(187.0,18.0,-99.8);
	glEnd();

	//pintu kanan ----------------------------------------------
	glBegin(GL_POLYGON);
	glColor3f (99.0/225.0, 112.0/225.0, 118.0/225.0);
	glVertex3f(180.0,-100.0,-99.8);
	glVertex3f(102.0,-100.0,-99.8);
	glVertex3f(102.0,0.0,-99.8);
	glVertex3f(180.0,0.0,-99.8);
	glEnd();

	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(92.0/255.0, 65.0/255.0, 48.0/255.0);
	glVertex3f(180.0,0.0,-99.5);
	glVertex3f(102.0,0.0,-99.5);
	glVertex3f(180.0,0.0,-99.5);
	glVertex3f(180.0,-100.0,-99.5);
	glVertex3f(102.0,0.0,-99.5);
	glVertex3f(102.0,-100.0,-99.5);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(92.0/255.0, 65.0/255.0, 48.0/255.0);
	glVertex3f(141.0,0.0,-99.5);
	glVertex3f(141.0,-100.0,-99.5);
	glEnd();
	glPointSize(3);
	glColor3f(92.0/255.0, 65.0/255.0, 48.0/255.0);
	glBegin(GL_POINTS);
	glVertex3f(150.0, -50.0, -99.5);
	glVertex3f(131.0, -50.0, -99.5);
	glEnd();


}
void jendelakiri()
{
    //jendela tembok depan
    glBegin(GL_POLYGON);//jendela 1 atas -------------------------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-735,175.0,-2.5);
	glVertex3f(-735,110.0,-2.5);
	glVertex3f(-710,110.0,-7.0);
	glVertex3f(-710,175.0,-7.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-735,175.0,-2.5);
	glVertex3f(-735,110.0,-2.5);
	glVertex3f(-710,110.0,-7.0);
	glVertex3f(-710,175.0,-7.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-720,175.0,-5.2);
	glVertex3f(-720,110.0,-5.2);
	glVertex3f(-710,110.0,-7.0);
	glVertex3f(-710,142.0,-7.0);
	glVertex3f(-735,142.0,-2.5);
	glVertex3f(-735,175.0,-2.5);
	glEnd();

	//jendela 2 atas -------------------------------------------------------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-695,175.0,-10.0);
	glVertex3f(-695,110.0,-10.0);
	glVertex3f(-670,110.0,-14.0);
	glVertex3f(-670,175.0,-14.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-695,175.0,-10.0);
	glVertex3f(-695,110.0,-10.0);
	glVertex3f(-670,110.0,-14.0);
	glVertex3f(-670,175.0,-14.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-680,175.0,-12.3);
	glVertex3f(-680,110.0,-12.3);
	glVertex3f(-670,110.0,-14.0);
	glVertex3f(-670,142.0,-14.0);
	glVertex3f(-695,142.0,-10.0);
	glVertex3f(-695,175.0,-10.0);
	glEnd();

	 //jendela 1 tengah -------------------------------------------------------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-735,85.0,-2.5);
	glVertex3f(-735,20.0,-2.5);
	glVertex3f(-710,20.0,-7.0);
	glVertex3f(-710,85.0,-7.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-735,85.0,-2.5);
	glVertex3f(-735,20.0,-2.5);
	glVertex3f(-710,20.0,-7.0);
	glVertex3f(-710,85.0,-7.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-720,85.0,-5.2);
	glVertex3f(-720,20.0,-5.2);
	glVertex3f(-710,20.0,-7.0);
	glVertex3f(-710,55.0,-7.0);
	glVertex3f(-735,55.0,-2.5);
	glVertex3f(-735,85.0,-2.5);
	glEnd();

	//jendela 2 tengah -------------------------------------------------------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-695,85.0,-10.0);
	glVertex3f(-695,20.0,-10.0);
	glVertex3f(-670,20.0,-14.0);
	glVertex3f(-670,85.0,-14.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-695,85.0,-10.0);
	glVertex3f(-695,20.0,-10.0);
	glVertex3f(-670,20.0,-14.0);
	glVertex3f(-670,85.0,-14.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-680,85.0,-12.3);
	glVertex3f(-680,20.0,-12.3);
	glVertex3f(-670,20.0,-14.0);
	glVertex3f(-670,55.0,-14.0);
	glVertex3f(-695,55.0,-10.0);
	glVertex3f(-695,85.0,-10.0);
	glEnd();

	//jendela 1 bawah -------------------------------------------------------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-735,-17.0,-2.5);
	glVertex3f(-735,-82.0,-2.5);
	glVertex3f(-710,-82.0,-7.0);
	glVertex3f(-710,-17.0,-7.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-735,-17.0,-2.5);
	glVertex3f(-735,-82.0,-2.5);
	glVertex3f(-710,-82.0,-7.0);
	glVertex3f(-710,-17.0,-7.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-720,-17.0,-5.2);
	glVertex3f(-720,-82.0,-5.2);
	glVertex3f(-710,-82.0,-7.0);
	glVertex3f(-710,-49.0,-7.0);
	glVertex3f(-735,-49.0,-2.5);
	glVertex3f(-735,-17.0,-2.5);
	glEnd();

	//jendela 2 bawah ----------------------------------------------ganti pintu---------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-695,-17.0,-10.0);
	glVertex3f(-695,-82.0,-10.0);
	glVertex3f(-670,-82.0,-14.0);
	glVertex3f(-670,-17.0,-14.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-695,-17.0,-10.0);
	glVertex3f(-695,-82.0,-10.0);
	glVertex3f(-670,-82.0,-14.0);
	glVertex3f(-670,-17.0,-14.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-680,-17.0,-12.3);
	glVertex3f(-680,-82.0,-12.3);
	glVertex3f(-670,-82.0,-14.0);
	glVertex3f(-670,-49.0,-14.0);
	glVertex3f(-695,-49.0,-10.0);
	glVertex3f(-695,-17.0,-10.0);
	glEnd();

	//tembok tengah
		//pintu-------------------------------------
	glLineWidth(4);
	glBegin(GL_LINES);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-507.5,-100.0,-14.3);
	glVertex3f(-507.5,0.0,-14.3);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-545.0,0.0,-7.8);
	glVertex3f(-545.0,-100.0,-7.8);
	glVertex3f(-470.0,-100.0,-20.9);
	glVertex3f(-470.0,0.0,-20.9);
	glEnd();
    glPointSize(4);
    glColor3f(0.0,0.0,0.0);
    glBegin(GL_POINTS);
    glVertex3f(-500.0,-65.0,-15.2);
    glEnd();
	glBegin(GL_POLYGON);//atas1
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-475.0,-10.0,-19.8);
	glVertex3f(-490.0,-10.0,-17.5);
	glVertex3f(-490.0,-25.0,-17.5);
	glVertex3f(-475.0,-25.0,-19.8);
	glEnd();
	glBegin(GL_POLYGON);//bawah1
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-475.0,-35.0,-19.8);
	glVertex3f(-490.0,-35.0,-17.5);
	glVertex3f(-490.0,-50.0,-17.5);
	glVertex3f(-475.0,-50.0,-19.8);
	glEnd();
	glBegin(GL_POLYGON);//atas2
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-492.0,-10.0,-16.8);
	glVertex3f(-500.0,-10.0,-15.5);
	glVertex3f(-500.0,-25.0,-15.5);
	glVertex3f(-492.0,-25.0,-16.8);
	glEnd();
	glBegin(GL_POLYGON);//bawah2
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-492.0,-35.0,-16.8);
	glVertex3f(-500.0,-35.0,-15.5);
	glVertex3f(-500.0,-50.0,-15.5);
	glVertex3f(-492.0,-50.0,-16.8);
	glEnd();
	glBegin(GL_POLYGON);//atas3
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-509.0,-10.0,-13.8);
	glVertex3f(-524.0,-10.0,-11.5);
	glVertex3f(-524.0,-25.0,-11.5);
	glVertex3f(-509.0,-25.0,-13.8);
	glEnd();
	glBegin(GL_POLYGON);//bawah3
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-509.0,-35.0,-13.8);
	glVertex3f(-524.0,-35.0,-11.5);
	glVertex3f(-524.0,-50.0,-11.5);
	glVertex3f(-509.0,-50.0,-13.8);
	glEnd();
	glBegin(GL_POLYGON);//atas4
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-526.0,-10.0,-10.8);
	glVertex3f(-541.0,-10.0,-8.5);
	glVertex3f(-541.0,-25.0,-8.5);
	glVertex3f(-526.0,-25.0,-10.8);
	glEnd();
	glBegin(GL_POLYGON);//bawah4
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-526.0,-35.0,-10.8);
	glVertex3f(-541.0,-35.0,-8.5);
	glVertex3f(-541.0,-50.0,-8.5);
	glVertex3f(-526.0,-50.0,-10.8);
	glEnd();

	glBegin(GL_POLYGON);//jendela 1 atas--------------------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-580.0,225.0,-1.5);
	glVertex3f(-580.0,140.0,-1.5);
	glVertex3f(-545.0,140.0,-7.3);
	glVertex3f(-545.0,225.0,-7.3);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-580.0,225.0,-1.5);
	glVertex3f(-580.0,140.0,-1.5);
	glVertex3f(-545.0,140.0,-7.3);
	glVertex3f(-545.0,225.0,-7.3);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-560.0,225.0,-4.8);
    glVertex3f(-560.0,140.0,-4.8);
    glVertex3f(-545.0,140.0,-7.3);
    glVertex3f(-545.0,185.0,-7.3);
    glVertex3f(-580.0,185.0,-1.5);
    glVertex3f(-580.0,225.0,-1.5);
	glEnd();

    glBegin(GL_POLYGON);//jendela 2 atas------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-530.0,225.0,-9.0);
	glVertex3f(-530.0,140.0,-9.0);
	glVertex3f(-490.0,140.0,-15.5);
	glVertex3f(-490.0,225.0,-15.5);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-530.0,225.0,-9.0);
	glVertex3f(-530.0,140.0,-9.0);
	glVertex3f(-490.0,140.0,-15.5);
	glVertex3f(-490.0,225.0,-15.5);
	glVertex3f(-530.0,225.0,-9.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-510.5,225.0,-12.2);
    glVertex3f(-510.5,140.0,-12.2);
    glVertex3f(-490.0,140.0,-15.5);
    glVertex3f(-490.0,185.0,-15.5);
    glVertex3f(-530.0,185.0,-9.0);
    glVertex3f(-530.0,225.0,-9.0);
	glEnd();

	glBegin(GL_POLYGON);//jendela 3 atas------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-475.0,225.0,-19.0);
	glVertex3f(-475.0,140.0,-19.0);
	glVertex3f(-435.0,140.0,-26.5);
	glVertex3f(-435.0,225.0,-26.5);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-475.0,225.0,-19.0);
	glVertex3f(-475.0,140.0,-19.0);
	glVertex3f(-435.0,140.0,-26.5);
	glVertex3f(-435.0,225.0,-26.5);
	glEnd();
    glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-453.0,225.0,-22.9);
    glVertex3f(-453.0,140.0,-22.9);
    glVertex3f(-435.0,140.0,-26.5);
    glVertex3f(-435.0,185.0,-26.5);
    glVertex3f(-475.0,185.0,-19.0);
    glVertex3f(-475.0,225.0,-19.0);
	glEnd();

	glBegin(GL_POLYGON);//jendela 1 tengah--------------------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-580.0,105.0,-1.5);
	glVertex3f(-580.0,25.0,-1.5);
	glVertex3f(-545.0,25.0,-7.3);
	glVertex3f(-545.0,105.0,-7.3);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-580.0,105.0,-1.5);
	glVertex3f(-580.0,25.0,-1.5);
	glVertex3f(-545.0,25.0,-7.3);
	glVertex3f(-545.0,105.0,-7.3);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-560.0,105.0,-4.8);
    glVertex3f(-560.0,25.0,-4.8);
    glVertex3f(-545.0,25.0,-7.3);
    glVertex3f(-545.0,65.0,-7.3);
    glVertex3f(-580.0,65.0,-1.5);
    glVertex3f(-580.0,105.0,-1.5);
	glEnd();
	 glBegin(GL_POLYGON);//jendela 2 tengah------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-530.0,105.0,-9.1);
	glVertex3f(-530.0,25.0,-9.1);
	glVertex3f(-490.0,25.0,-15.5);
	glVertex3f(-490.0,105.0,-15.5);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-530.0,105.0,-9.1);
	glVertex3f(-530.0,25.0,-9.1);
	glVertex3f(-490.0,25.0,-15.5);
	glVertex3f(-490.0,105.0,-15.5);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-510.0,105.0,-12.2);
    glVertex3f(-510.0,25.0,-12.2);
    glVertex3f(-490.0,25.0,-15.5);
    glVertex3f(-490.0,65.0,-15.5);
    glVertex3f(-530.0,65.0,-9.0);
    glVertex3f(-530.0,105.0,-9.0);
	glEnd();

	glBegin(GL_POLYGON);//jendela 3 tengah------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-475.0,105.0,-19.0);
	glVertex3f(-475.0,25.0,-19.0);
	glVertex3f(-435.0,25.0,-26.5);
	glVertex3f(-435.0,105.0,-26.5);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-475.0,105.0,-19.0);
	glVertex3f(-475.0,25.0,-19.0);
	glVertex3f(-435.0,25.0,-26.5);
	glVertex3f(-435.0,105.0,-26.5);
	glEnd();
    glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-453.0,105.0,-22.9);
    glVertex3f(-453.0,25.0,-22.9);
    glVertex3f(-435.0,25.0,-26.5);
    glVertex3f(-435.0,65.0,-26.5);
    glVertex3f(-475.0,65.0,-19.0);
    glVertex3f(-475.0,105.0,-19.0);
	glEnd();
	//jendela belakang
	glBegin(GL_POLYGON);//atas1 --------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-470.0,175.0,-51.5);
	glVertex3f(-470.0,110.0,-51.5);
	glVertex3f(-440.0,110.0,-57.2);
	glVertex3f(-440.0,175.0,-57.2);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-470.0,175.0,-51.5);
	glVertex3f(-470.0,110.0,-51.5);
	glVertex3f(-440.0,110.0,-57.2);
	glVertex3f(-440.0,175.0,-57.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-455.0,175.0,-54.3);
	glVertex3f(-455.0,110.0,-54.3);
	glVertex3f(-470.0,142.5,-51.4);
	glVertex3f(-440.0,142.5,-57.1);
	glEnd();
	glBegin(GL_POLYGON);//atas2 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-420.0,175.0,-60.0);
	glVertex3f(-420.0,110.0,-60.0);
	glVertex3f(-365.0,110.0,-69.8);
	glVertex3f(-365.0,175.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-420.0,175.0,-60.0);
	glVertex3f(-420.0,110.0,-60.0);
	glVertex3f(-365.0,110.0,-69.8);
	glVertex3f(-365.0,175.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-392.5,175.0,-64.7);
	glVertex3f(-392.5,110.0,-64.7);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-419.5,142.0,-60.0);
	glVertex3f(-365.0,142.0,-69.8);
	glVertex3f(-405.0,175.0,-62.5);
	glVertex3f(-405.0,110.0,-62.5);
	glVertex3f(-377.0,175.0,-67.0);
	glVertex3f(-377.0,110.0,-67.0);
	glEnd();
	glBegin(GL_POLYGON);//atas3 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-345.0,175.0,-75.0);
	glVertex3f(-345.0,110.0,-75.0);
	glVertex3f(-290.0,110.0,-83.8);
	glVertex3f(-290.0,175.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-345.0,175.0,-75.0);
	glVertex3f(-345.0,110.0,-75.0);
	glVertex3f(-290.0,110.0,-83.8);
	glVertex3f(-290.0,175.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-317.5,175.0,-79.2);
	glVertex3f(-317.5,110.0,-79.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-331.5,175.0,-77.0);
	glVertex3f(-331.5,110.0,-77.0);
	glVertex3f(-303.0,175.0,-81.0);
	glVertex3f(-303.0,110.0,-81.0);
	glVertex3f(-343.0,142.0,-75.0);
	glVertex3f(-290.0,142.0,-83.8);
	glEnd();
	glBegin(GL_POLYGON);//atas4 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-270.0,175.0,-86.5);
	glVertex3f(-270.0,110.0,-86.5);
	glVertex3f(-220.0,110.0,-95.6);
	glVertex3f(-220.0,175.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-270.0,175.0,-86.5);
	glVertex3f(-270.0,110.0,-86.5);
	glVertex3f(-220.0,110.0,-95.6);
	glVertex3f(-220.0,175.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-245.5,175.0,-90.8);
	glVertex3f(-245.5,110.0,-90.8);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-231.0,175.0,-93.1);
	glVertex3f(-231.0,110.0,-93.1);
	glVertex3f(-258.0,175.0,-88.5);
	glVertex3f(-258.0,110.0,-88.5);
	glVertex3f(-269.0,142.0,-86.5);
	glVertex3f(-220.0,142.0,-95.6);
	glEnd();

	glBegin(GL_POLYGON);//tengah 1
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-470.0,80.0,-51.5);
	glVertex3f(-470.0,20.0,-51.5);
	glVertex3f(-440.0,20.0,-57.2);
	glVertex3f(-440.0,80.0,-57.2);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-470.0,80.0,-51.5);
	glVertex3f(-470.0,20.0,-51.5);
	glVertex3f(-440.0,20.0,-57.2);
	glVertex3f(-440.0,80.0,-57.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-455.0,80.0,-54.3);
	glVertex3f(-455.0,20.0,-54.3);
	glVertex3f(-470.0,49.0,-51.4);
	glVertex3f(-440.0,49.0,-57.1);
	glEnd();

	glBegin(GL_POLYGON);//tengah2 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-420.0,80.0,-60.0);
	glVertex3f(-420.0,20.0,-60.0);
	glVertex3f(-365.0,20.0,-69.8);
	glVertex3f(-365.0,80.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-420.0,80.0,-60.0);
	glVertex3f(-420.0,20.0,-60.0);
	glVertex3f(-365.0,20.0,-69.8);
	glVertex3f(-365.0,80.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-392.5,80.0,-64.7);
	glVertex3f(-392.5,20.0,-64.7);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-419.5,47.5,-60.0);
	glVertex3f(-365.0,47.5,-69.8);
	glVertex3f(-405.0,80.0,-62.5);
	glVertex3f(-405.0,20.0,-62.5);
	glVertex3f(-377.0,80.0,-67.0);
	glVertex3f(-377.0,20.0,-67.0);
	glEnd();

	glBegin(GL_POLYGON);//tengah3 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-345.0,80.0,-75.0);
	glVertex3f(-345.0,20.0,-75.0);
	glVertex3f(-290.0,20.0,-83.8);
	glVertex3f(-290.0,80.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-345.0,80.0,-75.0);
	glVertex3f(-345.0,20.0,-75.0);
	glVertex3f(-290.0,20.0,-83.8);
	glVertex3f(-290.0,80.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-317.5,80.0,-79.2);
	glVertex3f(-317.5,20.0,-79.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-331.5,80.0,-77.0);
	glVertex3f(-331.5,20.0,-77.0);
	glVertex3f(-303.0,80.0,-81.0);
	glVertex3f(-303.0,20.0,-81.0);
	glVertex3f(-343.0,49.0,-75.0);
	glVertex3f(-290.0,49.0,-83.8);
	glEnd();
	glBegin(GL_POLYGON);//tengah4 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-270.0,80.0,-86.5);
	glVertex3f(-270.0,20.0,-86.5);
	glVertex3f(-220.0,20.0,-95.6);
	glVertex3f(-220.0,80.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-270.0,80.0,-86.5);
	glVertex3f(-270.0,20.0,-86.5);
	glVertex3f(-220.0,20.0,-95.6);
	glVertex3f(-220.0,80.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-245.5,80.0,-90.8);
	glVertex3f(-245.5,20.0,-90.8);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-231.0,80.0,-93.1);
	glVertex3f(-231.0,20.0,-93.1);
	glVertex3f(-258.0,80.0,-88.5);
	glVertex3f(-258.0,20.0,-88.5);
	glVertex3f(-269.0,49.0,-86.5);
	glVertex3f(-220.0,49.0,-95.6);
	glEnd();

	glBegin(GL_POLYGON);//bawah1 --------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-470.0,-17.0,-51.5);
	glVertex3f(-470.0,-82.0,-51.5);
	glVertex3f(-440.0,-82.0,-57.2);
	glVertex3f(-440.0,-17.0,-57.2);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-470.0,-17.0,-51.5);
	glVertex3f(-470.0,-82.0,-51.5);
	glVertex3f(-440.0,-82.0,-57.2);
	glVertex3f(-440.0,-17.0,-57.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-455.0,-82.0,-54.3);
	glVertex3f(-455.0,-17.0,-54.3);
	glVertex3f(-470.0,-49,-51.4);
	glVertex3f(-440.0,-49.5,-57.1);
	glEnd();
	glBegin(GL_POLYGON);//bawah2 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-420.0,-17.0,-60.0);
	glVertex3f(-420.0,-82.0,-60.0);
	glVertex3f(-365.0,-82.0,-69.8);
	glVertex3f(-365.0,-17.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-420.0,-17.0,-60.0);
	glVertex3f(-420.0,-82.0,-60.0);
	glVertex3f(-365.0,-82.0,-69.8);
	glVertex3f(-365.0,-17.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-392.5,-17.0,-64.7);
	glVertex3f(-392.5,-82.0,-64.7);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-419.5,-49.5,-60.0);
	glVertex3f(-365.0,-49.5,-69.8);
	glVertex3f(-405.0,-17.0,-62.5);
	glVertex3f(-405.0,-82.0,-62.5);
	glVertex3f(-377.0,-17.0,-67.0);
	glVertex3f(-377.0,-82.0,-67.0);
	glEnd();
	glBegin(GL_POLYGON);//bawah3 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-345.0,-17.0,-75.0);
	glVertex3f(-345.0,-82.0,-75.0);
	glVertex3f(-290.0,-82.0,-83.8);
	glVertex3f(-290.0,-17.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-345.0,-17.0,-75.0);
	glVertex3f(-345.0,-82.0,-75.0);
	glVertex3f(-290.0,-82.0,-83.8);
	glVertex3f(-290.0,-17.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-317.5,-17.0,-79.2);
	glVertex3f(-317.5,-82.0,-79.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-331.5,-17.0,-77.0);
	glVertex3f(-331.5,-82.0,-77.0);
	glVertex3f(-303.0,-17.0,-81.0);
	glVertex3f(-303.0,-82.0,-81.0);
	glVertex3f(-343.0,-50.0,-75.0);
	glVertex3f(-290.0,-50.0,-83.8);
	glEnd();
	glBegin(GL_POLYGON);//atas4 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-270.0,-17.0,-86.5);
	glVertex3f(-270.0,-82.0,-86.5);
	glVertex3f(-220.0,-82.0,-95.6);
	glVertex3f(-220.0,-17.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-270.0,-82.0,-86.5);
	glVertex3f(-270.0,-17.0,-86.5);
	glVertex3f(-220.0,-17.0,-95.6);
	glVertex3f(-220.0,-82.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-245.5,-17.0,-90.8);
	glVertex3f(-245.5,-82.0,-90.8);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-231.0,-17.0,-93.1);
	glVertex3f(-231.0,-82.0,-93.1);
	glVertex3f(-258.0,-17.0,-88.5);
	glVertex3f(-258.0,-82.0,-88.5);
	glVertex3f(-269.0,-50.0,-86.5);
	glVertex3f(-220.0,-50.0,-95.6);
	glEnd();

}
void jendelakanan()
{
    //jendela tembok depan
    glBegin(GL_POLYGON);//jendela 1 atas -------------------------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(735,175.0,-2.5);
	glVertex3f(735,110.0,-2.5);
	glVertex3f(710,110.0,-7.0);
	glVertex3f(710,175.0,-7.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(735,175.0,-2.5);
	glVertex3f(735,110.0,-2.5);
	glVertex3f(710,110.0,-7.0);
	glVertex3f(710,175.0,-7.0);
	glVertex3f(735,175.0,-2.5);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(720,175.0,-5.2);
	glVertex3f(720,110.0,-5.2);
	glVertex3f(710,110.0,-7.0);
	glVertex3f(710,142.0,-7.0);
	glVertex3f(735,142.0,-2.5);
	glVertex3f(735,175.0,-2.5);
	glEnd();

	//jendela 2 atas -------------------------------------------------------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(695,175.0,-10.0);
	glVertex3f(695,110.0,-10.0);
	glVertex3f(670,110.0,-14.0);
	glVertex3f(670,175.0,-14.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(695,175.0,-10.0);
	glVertex3f(695,110.0,-10.0);
	glVertex3f(670,110.0,-14.0);
	glVertex3f(670,175.0,-14.0);
	glVertex3f(695,175.0,-10.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(680,175.0,-12.3);
	glVertex3f(680,110.0,-12.3);
	glVertex3f(670,110.0,-14.0);
	glVertex3f(670,142.0,-14.0);
	glVertex3f(695,142.0,-10.0);
	glVertex3f(695,175.0,-10.0);
	glEnd();



	 //jendela 1 tengah -------------------------------------------------------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(735,85.0,-2.5);
	glVertex3f(735,20.0,-2.5);
	glVertex3f(710,20.0,-7.0);
	glVertex3f(710,85.0,-7.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(735,85.0,-2.5);
	glVertex3f(735,20.0,-2.5);
	glVertex3f(710,20.0,-7.0);
	glVertex3f(710,85.0,-7.0);
	glVertex3f(735,85.0,-2.5);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(720,85.0,-5.2);
	glVertex3f(720,20.0,-5.2);
	glVertex3f(710,20.0,-7.0);
	glVertex3f(710,55.0,-7.0);
	glVertex3f(735,55.0,-2.5);
	glVertex3f(735,85.0,-2.5);
	glEnd();

	//jendela 2 tengah -------------------------------------------------------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(695,85.0,-10.0);
	glVertex3f(695,20.0,-10.0);
	glVertex3f(670,20.0,-14.0);
	glVertex3f(670,85.0,-14.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(695,85.0,-10.0);
	glVertex3f(695,20.0,-10.0);
	glVertex3f(670,20.0,-14.0);
	glVertex3f(670,85.0,-14.0);
	glVertex3f(695,85.0,-10.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(680,85.0,-12.3);
	glVertex3f(680,20.0,-12.3);
	glVertex3f(670,20.0,-14.0);
	glVertex3f(670,55.0,-14.0);
	glVertex3f(695,55.0,-10.0);
	glVertex3f(695,85.0,-10.0);
	glEnd();

	//jendela 1 bawah -------------------------------------------------------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(735,-17.0,-2.5);
	glVertex3f(735,-82.0,-2.5);
	glVertex3f(710,-82.0,-7.0);
	glVertex3f(710,-17.0,-7.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(735,-17.0,-2.5);
	glVertex3f(735,-82.0,-2.5);
	glVertex3f(710,-82.0,-7.0);
	glVertex3f(710,-17.0,-7.0);
	glVertex3f(735,-17.0,-2.5);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(720,-17.0,-5.2);
	glVertex3f(720,-82.0,-5.2);
	glVertex3f(710,-82.0,-7.0);
	glVertex3f(710,-49.0,-7.0);
	glVertex3f(735,-49.0,-2.5);
	glVertex3f(735,-17.0,-2.5);
	glEnd();
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(695,-17.0,-10.0);
	glVertex3f(695,-82.0,-10.0);
	glVertex3f(670,-82.0,-14.0);
	glVertex3f(670,-17.0,-14.0);
    glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(695,-17.0,-10.0);
	glVertex3f(695,-82.0,-10.0);
	glVertex3f(670,-82.0,-14.0);
	glVertex3f(670,-17.0,-14.0);
	glVertex3f(695,-17.0,-10.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(680,-17.0,-12.3);
	glVertex3f(680,-82.0,-12.3);
	glVertex3f(670,-82.0,-14.0);
	glVertex3f(670,-49.0,-14.0);
	glVertex3f(695,-49.0,-10.0);
	glVertex3f(695,-17.0,-10.0);
	glEnd();

	//tembok tengah
	//pintu-------------------------------------
	glLineWidth(4);
	glBegin(GL_LINES);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(507.5,-100.0,-14.3);
	glVertex3f(507.5,0.0,-14.3);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(545.0,0.0,-7.8);
	glVertex3f(545.0,-100.0,-7.8);
	glVertex3f(470.0,-100.0,-20.9);
	glVertex3f(470.0,0.0,-20.9);
	glEnd();
    glPointSize(4);
    glColor3f(0.0,0.0,0.0);
    glBegin(GL_POINTS);
    glVertex3f(500.0,-65.0,-15.2);
    glEnd();
	glBegin(GL_POLYGON);//atas1
	glColor3f(0.0,0.0,0.0);
	glVertex3f(475.0,-10.0,-19.8);
	glVertex3f(490.0,-10.0,-17.5);
	glVertex3f(490.0,-25.0,-17.5);
	glVertex3f(475.0,-25.0,-19.8);
	glEnd();
	glBegin(GL_POLYGON);//bawah1
	glColor3f(0.0,0.0,0.0);
	glVertex3f(475.0,-35.0,-19.8);
	glVertex3f(490.0,-35.0,-17.5);
	glVertex3f(490.0,-50.0,-17.5);
	glVertex3f(475.0,-50.0,-19.8);
	glEnd();
	glBegin(GL_POLYGON);//atas2
	glColor3f(0.0,0.0,0.0);
	glVertex3f(492.0,-10.0,-16.8);
	glVertex3f(500.0,-10.0,-15.5);
	glVertex3f(500.0,-25.0,-15.5);
	glVertex3f(492.0,-25.0,-16.8);
	glEnd();
	glBegin(GL_POLYGON);//bawah2
	glColor3f(0.0,0.0,0.0);
	glVertex3f(492.0,-35.0,-16.8);
	glVertex3f(500.0,-35.0,-15.5);
	glVertex3f(500.0,-50.0,-15.5);
	glVertex3f(492.0,-50.0,-16.8);
	glEnd();
	glBegin(GL_POLYGON);//atas3
	glColor3f(0.0,0.0,0.0);
	glVertex3f(509.0,-10.0,-13.8);
	glVertex3f(524.0,-10.0,-11.5);
	glVertex3f(524.0,-25.0,-11.5);
	glVertex3f(509.0,-25.0,-13.8);
	glEnd();
	glBegin(GL_POLYGON);//bawah3
	glColor3f(0.0,0.0,0.0);
	glVertex3f(509.0,-35.0,-13.8);
	glVertex3f(524.0,-35.0,-11.5);
	glVertex3f(524.0,-50.0,-11.5);
	glVertex3f(509.0,-50.0,-13.8);
	glEnd();
	glBegin(GL_POLYGON);//atas4
	glColor3f(0.0,0.0,0.0);
	glVertex3f(526.0,-10.0,-10.8);
	glVertex3f(541.0,-10.0,-8.5);
	glVertex3f(541.0,-25.0,-8.5);
	glVertex3f(526.0,-25.0,-10.8);
	glEnd();
	glBegin(GL_POLYGON);//bawah4
	glColor3f(0.0,0.0,0.0);
	glVertex3f(526.0,-35.0,-10.8);
	glVertex3f(541.0,-35.0,-8.5);
	glVertex3f(541.0,-50.0,-8.5);
	glVertex3f(526.0,-50.0,-10.8);
	glEnd();

	glBegin(GL_POLYGON);//jendela 1 atas--------------------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(580.0,225.0,-1.5);
	glVertex3f(580.0,140.0,-1.5);
	glVertex3f(545.0,140.0,-7.3);
	glVertex3f(545.0,225.0,-7.3);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(580.0,225.0,-1.5);
	glVertex3f(580.0,140.0,-1.5);
	glVertex3f(545.0,140.0,-7.3);
	glVertex3f(545.0,225.0,-7.3);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(560.0,225.0,-4.8);
    glVertex3f(560.0,140.0,-4.8);
    glVertex3f(545.0,140.0,-7.3);
    glVertex3f(545.0,185.0,-7.3);
    glVertex3f(580.0,185.0,-1.5);
    glVertex3f(580.0,225.0,-1.5);
	glEnd();

    glBegin(GL_POLYGON);//jendela 2 atas------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(530.0,225.0,-9.0);
	glVertex3f(530.0,140.0,-9.0);
	glVertex3f(490.0,140.0,-15.5);
	glVertex3f(490.0,225.0,-15.5);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(530.0,225.0,-9.0);
	glVertex3f(530.0,140.0,-9.0);
	glVertex3f(490.0,140.0,-15.5);
	glVertex3f(490.0,225.0,-15.5);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(510.5,225.0,-12.2);
    glVertex3f(510.5,140.0,-12.2);
    glVertex3f(490.0,140.0,-15.5);
    glVertex3f(490.0,185.0,-15.5);
    glVertex3f(530.0,185.0,-9.0);
    glVertex3f(530.0,225.0,-9.0);
	glEnd();

	glBegin(GL_POLYGON);//jendela 3 atas------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(475.0,225.0,-19.0);
	glVertex3f(475.0,140.0,-19.0);
	glVertex3f(435.0,140.0,-26.5);
	glVertex3f(435.0,225.0,-26.5);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(475.0,225.0,-19.0);
	glVertex3f(475.0,140.0,-19.0);
	glVertex3f(435.0,140.0,-26.5);
	glVertex3f(435.0,225.0,-26.5);
	glEnd();
    glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(453.0,225.0,-22.9);
    glVertex3f(453.0,140.0,-22.9);
    glVertex3f(435.0,140.0,-26.5);
    glVertex3f(435.0,185.0,-26.5);
    glVertex3f(475.0,185.0,-19.0);
    glVertex3f(475.0,225.0,-19.0);
	glEnd();

	glBegin(GL_POLYGON);//jendela 1 tengah--------------------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(580.0,105.0,-1.5);
	glVertex3f(580.0,25.0,-1.5);
	glVertex3f(545.0,25.0,-7.3);
	glVertex3f(545.0,105.0,-7.3);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(580.0,105.0,-1.5);
	glVertex3f(580.0,25.0,-1.5);
	glVertex3f(545.0,25.0,-7.3);
	glVertex3f(545.0,105.0,-7.3);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(560.0,105.0,-4.8);
    glVertex3f(560.0,25.0,-4.8);
    glVertex3f(545.0,25.0,-7.3);
    glVertex3f(545.0,65.0,-7.3);
    glVertex3f(580.0,65.0,-1.5);
    glVertex3f(580.0,105.0,-1.5);
	glEnd();
	 glBegin(GL_POLYGON);//jendela 2 tengah------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(530.0,105.0,-9.1);
	glVertex3f(530.0,25.0,-9.1);
	glVertex3f(490.0,25.0,-15.5);
	glVertex3f(490.0,105.0,-15.5);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(530.0,105.0,-9.1);
	glVertex3f(530.0,25.0,-9.1);
	glVertex3f(490.0,25.0,-15.5);
	glVertex3f(490.0,105.0,-15.5);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(510.0,105.0,-12.2);
    glVertex3f(510.0,25.0,-12.2);
    glVertex3f(490.0,25.0,-15.5);
    glVertex3f(490.0,65.0,-15.5);
    glVertex3f(530.0,65.0,-9.0);
    glVertex3f(530.0,105.0,-9.0);
	glEnd();

	glBegin(GL_POLYGON);//jendela 3 tengah------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(475.0,105.0,-19.0);
	glVertex3f(475.0,25.0,-19.0);
	glVertex3f(435.0,25.0,-26.5);
	glVertex3f(435.0,105.0,-26.5);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(475.0,105.0,-19.0);
	glVertex3f(475.0,25.0,-19.0);
	glVertex3f(435.0,25.0,-26.5);
	glVertex3f(435.0,105.0,-26.5);
	glEnd();
    glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(453.0,105.0,-22.9);
    glVertex3f(453.0,25.0,-22.9);
    glVertex3f(435.0,25.0,-26.5);
    glVertex3f(435.0,65.0,-26.5);
    glVertex3f(475.0,65.0,-19.0);
    glVertex3f(475.0,105.0,-19.0);
	glEnd();

	//jendela belakang
	glBegin(GL_POLYGON);//atas1 --------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(470.0,175.0,-51.5);
	glVertex3f(470.0,110.0,-51.5);
	glVertex3f(440.0,110.0,-57.2);
	glVertex3f(440.0,175.0,-57.2);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(470.0,175.0,-51.5);
	glVertex3f(470.0,110.0,-51.5);
	glVertex3f(440.0,110.0,-57.2);
	glVertex3f(440.0,175.0,-57.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(455.0,175.0,-54.3);
	glVertex3f(455.0,110.0,-54.3);
	glVertex3f(470.0,142.5,-51.4);
	glVertex3f(440.0,142.5,-57.1);
	glEnd();
	glBegin(GL_POLYGON);//atas2 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(420.0,175.0,-60.0);
	glVertex3f(420.0,110.0,-60.0);
	glVertex3f(365.0,110.0,-69.8);
	glVertex3f(365.0,175.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(420.0,175.0,-60.0);
	glVertex3f(420.0,110.0,-60.0);
	glVertex3f(365.0,110.0,-69.8);
	glVertex3f(365.0,175.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(392.5,175.0,-64.7);
	glVertex3f(392.5,110.0,-64.7);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(419.5,142.0,-60.0);
	glVertex3f(365.0,142.0,-69.8);
	glVertex3f(405.0,175.0,-62.5);
	glVertex3f(405.0,110.0,-62.5);
	glVertex3f(377.0,175.0,-67.0);
	glVertex3f(377.0,110.0,-67.0);
	glEnd();
	glBegin(GL_POLYGON);//atas3 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(345.0,175.0,-75.0);
	glVertex3f(345.0,110.0,-75.0);
	glVertex3f(290.0,110.0,-83.8);
	glVertex3f(290.0,175.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(345.0,175.0,-75.0);
	glVertex3f(345.0,110.0,-75.0);
	glVertex3f(290.0,110.0,-83.8);
	glVertex3f(290.0,175.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(317.5,175.0,-79.2);
	glVertex3f(317.5,110.0,-79.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(331.5,175.0,-77.0);
	glVertex3f(331.5,110.0,-77.0);
	glVertex3f(303.0,175.0,-81.0);
	glVertex3f(303.0,110.0,-81.0);
	glVertex3f(343.0,142.0,-75.0);
	glVertex3f(290.0,142.0,-83.8);
	glEnd();
	glBegin(GL_POLYGON);//atas4 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(270.0,175.0,-86.5);
	glVertex3f(270.0,110.0,-86.5);
	glVertex3f(220.0,110.0,-95.6);
	glVertex3f(220.0,175.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(270.0,175.0,-86.5);
	glVertex3f(270.0,110.0,-86.5);
	glVertex3f(220.0,110.0,-95.6);
	glVertex3f(220.0,175.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(245.5,175.0,-90.8);
	glVertex3f(245.5,110.0,-90.8);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(231.0,175.0,-93.1);
	glVertex3f(231.0,110.0,-93.1);
	glVertex3f(258.0,175.0,-88.5);
	glVertex3f(258.0,110.0,-88.5);
	glVertex3f(269.0,142.0,-86.5);
	glVertex3f(220.0,142.0,-95.6);
	glEnd();

	glBegin(GL_POLYGON);//tengah 1
	glColor3f(0.0,0.0,0.0);
	glVertex3f(470.0,80.0,-51.5);
	glVertex3f(470.0,20.0,-51.5);
	glVertex3f(440.0,20.0,-57.2);
	glVertex3f(440.0,80.0,-57.2);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(470.0,80.0,-51.5);
	glVertex3f(470.0,20.0,-51.5);
	glVertex3f(440.0,20.0,-57.2);
	glVertex3f(440.0,80.0,-57.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(455.0,80.0,-54.3);
	glVertex3f(455.0,20.0,-54.3);
	glVertex3f(470.0,49.0,-51.4);
	glVertex3f(440.0,49.0,-57.1);
	glEnd();

	glBegin(GL_POLYGON);//tengah2 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(420.0,80.0,-60.0);
	glVertex3f(420.0,20.0,-60.0);
	glVertex3f(365.0,20.0,-69.8);
	glVertex3f(365.0,80.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(420.0,80.0,-60.0);
	glVertex3f(420.0,20.0,-60.0);
	glVertex3f(365.0,20.0,-69.8);
	glVertex3f(365.0,80.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(392.5,80.0,-64.7);
	glVertex3f(392.5,20.0,-64.7);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(419.5,47.5,-60.0);
	glVertex3f(365.0,47.5,-69.8);
	glVertex3f(405.0,80.0,-62.5);
	glVertex3f(405.0,20.0,-62.5);
	glVertex3f(377.0,80.0,-67.0);
	glVertex3f(377.0,20.0,-67.0);
	glEnd();

	glBegin(GL_POLYGON);//tengah3 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(345.0,80.0,-75.0);
	glVertex3f(345.0,20.0,-75.0);
	glVertex3f(290.0,20.0,-83.8);
	glVertex3f(290.0,80.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(345.0,80.0,-75.0);
	glVertex3f(345.0,20.0,-75.0);
	glVertex3f(290.0,20.0,-83.8);
	glVertex3f(290.0,80.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(317.5,80.0,-79.2);
	glVertex3f(317.5,20.0,-79.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(331.5,80.0,-77.0);
	glVertex3f(331.5,20.0,-77.0);
	glVertex3f(303.0,80.0,-81.0);
	glVertex3f(303.0,20.0,-81.0);
	glVertex3f(343.0,49.0,-75.0);
	glVertex3f(290.0,49.0,-83.8);
	glEnd();
	glBegin(GL_POLYGON);//tengah4 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(270.0,80.0,-86.5);
	glVertex3f(270.0,20.0,-86.5);
	glVertex3f(220.0,20.0,-95.6);
	glVertex3f(220.0,80.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(270.0,80.0,-86.5);
	glVertex3f(270.0,20.0,-86.5);
	glVertex3f(220.0,20.0,-95.6);
	glVertex3f(220.0,80.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(245.5,80.0,-90.8);
	glVertex3f(245.5,20.0,-90.8);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(231.0,80.0,-93.1);
	glVertex3f(231.0,20.0,-93.1);
	glVertex3f(258.0,80.0,-88.5);
	glVertex3f(258.0,20.0,-88.5);
	glVertex3f(269.0,49.0,-86.5);
	glVertex3f(220.0,49.0,-95.6);
	glEnd();

	glBegin(GL_POLYGON);//bawah1 --------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(470.0,-17.0,-51.5);
	glVertex3f(470.0,-82.0,-51.5);
	glVertex3f(440.0,-82.0,-57.2);
	glVertex3f(440.0,-17.0,-57.2);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(470.0,-17.0,-51.5);
	glVertex3f(470.0,-82.0,-51.5);
	glVertex3f(440.0,-82.0,-57.2);
	glVertex3f(440.0,-17.0,-57.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(455.0,-82.0,-54.3);
	glVertex3f(455.0,-17.0,-54.3);
	glVertex3f(470.0,-49,-51.4);
	glVertex3f(440.0,-49.5,-57.1);
	glEnd();
	glBegin(GL_POLYGON);//bawah2 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(420.0,-17.0,-60.0);
	glVertex3f(420.0,-82.0,-60.0);
	glVertex3f(365.0,-82.0,-69.8);
	glVertex3f(365.0,-17.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(420.0,-17.0,-60.0);
	glVertex3f(420.0,-82.0,-60.0);
	glVertex3f(365.0,-82.0,-69.8);
	glVertex3f(365.0,-17.0,-69.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(392.5,-17.0,-64.7);
	glVertex3f(392.5,-82.0,-64.7);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(419.5,-49.5,-60.0);
	glVertex3f(365.0,-49.5,-69.8);
	glVertex3f(405.0,-17.0,-62.5);
	glVertex3f(405.0,-82.0,-62.5);
	glVertex3f(377.0,-17.0,-67.0);
	glVertex3f(377.0,-82.0,-67.0);
	glEnd();
	glBegin(GL_POLYGON);//bawah3 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(345.0,-17.0,-75.0);
	glVertex3f(345.0,-82.0,-75.0);
	glVertex3f(290.0,-82.0,-83.8);
	glVertex3f(290.0,-17.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(345.0,-17.0,-75.0);
	glVertex3f(345.0,-82.0,-75.0);
	glVertex3f(290.0,-82.0,-83.8);
	glVertex3f(290.0,-17.0,-83.8);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(317.5,-17.0,-79.2);
	glVertex3f(317.5,-82.0,-79.2);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(331.5,-17.0,-77.0);
	glVertex3f(331.5,-82.0,-77.0);
	glVertex3f(303.0,-17.0,-81.0);
	glVertex3f(303.0,-82.0,-81.0);
	glVertex3f(343.0,-50.0,-75.0);
	glVertex3f(290.0,-50.0,-83.8);
	glEnd();
	glBegin(GL_POLYGON);//atas4 -------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(270.0,-17.0,-86.5);
	glVertex3f(270.0,-82.0,-86.5);
	glVertex3f(220.0,-82.0,-95.6);
	glVertex3f(220.0,-17.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(270.0,-82.0,-86.5);
	glVertex3f(270.0,-17.0,-86.5);
	glVertex3f(220.0,-17.0,-95.6);
	glVertex3f(220.0,-82.0,-95.6);
	glEnd();
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(245.5,-17.0,-90.8);
	glVertex3f(245.5,-82.0,-90.8);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINES);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(231.0,-17.0,-93.1);
	glVertex3f(231.0,-82.0,-93.1);
	glVertex3f(258.0,-17.0,-88.5);
	glVertex3f(258.0,-82.0,-88.5);
	glVertex3f(269.0,-50.0,-86.5);
	glVertex3f(220.0,-50.0,-95.6);
	glEnd();

}
void tabung()
{
	// gambar bayangan
	glPushMatrix();
	glTranslatef(0.5, 200.0, -50.0);
	glRotatef(45, 45, 0, 0);
	glRotatef(45, 45, 0, 0);
	glColor3f (184.0/255.0, 147.0/255.0, 120.0/255.0); //warna tabung

	qobj = gluNewQuadric();
    gluQuadricDrawStyle(qobj, GLU_FILL);

    gluCylinder(qobj, 40, 40, 300, 200, 90);
}
void paralon()
{
	//gedung kanan 
	glLineWidth(3);
	glBegin(GL_LINES);
	glColor3f(0,0,0);
	glVertex3f(210.0,-100.0,-99.0);
	glVertex3f(210.0,190.0,-99.0);
	glVertex3f(210.0,200.0,-60.0);
	glVertex3f(210.0,190.0,-99.0);

	glVertex3f(430.0,-100.0,-59.0);
	glVertex3f(430.0,190.0,-59.0);
	glVertex3f(430.0,190.0,-59.0);
	glVertex3f(300.0,200.0,-50.0);

	glVertex3f(744.8,-100.0,-1.0);
	glVertex3f(744.8,190.0,-1.0);
	glVertex3f(744.8,190.0,-1.0);
	glVertex3f(680.0,200.0,4.0);
	glEnd();

}
void kubah()
{
	//kubah depan
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 164.0/255., 159.0/255.);
	glVertex3f(-60.0,500.0,-190.0);
	glVertex3f(60.0,500.0,-190.0);
	glVertex3f(50.0,640.0,-190.0);
	glVertex3f(-50.0,640.0,-190.0);
	glEnd();
	//kubah belakang
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 164.0/255., 159.0/255.);
	glVertex3f(-60.0,500.0,-260.0);
	glVertex3f(60.0,500.0,-260.0);
	glVertex3f(50.0,640.0,-260.0);
	glVertex3f(-50.0,640.0,-260.0);
	glEnd();
	//kubah kiri
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 164.0/255., 159.0/255.);
	glVertex3f(-60.0,500.0,-190.0);
	glVertex3f(-60.0,500.0,-260.0);
	glVertex3f(-50.0,640.0,-260.0);
	glVertex3f(-50.0,640.0,-190.0);
	glEnd();
	//kubah kanan
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 164.0/255., 159.0/255.);
	glVertex3f(60.0,500.0,-190.0);
	glVertex3f(60.0,500.0,-260.0);
	glVertex3f(50.0,640.0,-260.0);
	glVertex3f(50.0,640.0,-190.0);
	glEnd();
	//tutup kubah
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 164.0/255., 159.0/255.);
	glVertex3f(-50.0,640.0,-190.0);
	glVertex3f(-50.0,640.0,-260.0);
	glVertex3f(50.0,640.0,-260.0);
	glVertex3f(50.0,640.0,-190.0);
	glEnd();
	//atasnya kubah++++++++++++++++++++++++++++++++++++++++++
	//atas depan
	glBegin(GL_POLYGON);
	glColor3f (103.0/255.0, 93.0/255., 84.0/255.);
	glVertex3f(-40.0,740.0,-200.0);
	glVertex3f(40.0,740.0,-200.0);
	glVertex3f(40.0,640.0,-200.0);
	glVertex3f(-40.0,640.0,-200.0);
	glEnd();
	//atas belakang
	glBegin(GL_POLYGON);
	glColor3f (103.0/255.0, 93.0/255., 84.0/255.);
	glVertex3f(-40.0,740.0,-250.0);
	glVertex3f(40.0,740.0,-250.0);
	glVertex3f(40.0,640.0,-250.0);
	glVertex3f(-40.0,640.0,-250.0);
	glEnd();
	//atas kubah kiri
	glBegin(GL_POLYGON);
	glColor3f (103.0/255.0, 93.0/255., 84.0/255.);
	glVertex3f(-40.0,740.0,-200.0);
	glVertex3f(-40.0,740.0,-250.0);
	glVertex3f(-40.0,640.0,-250.0);
	glVertex3f(-40.0,640.0,-200.0);
	glEnd();
	//atas kubah kanan
	glBegin(GL_POLYGON);
	glColor3f (103.0/255.0, 93.0/255., 84.0/255.);
	glVertex3f(40.0,740.0,-200.0);
	glVertex3f(40.0,740.0,-250.0);
	glVertex3f(40.0,640.0,-250.0);
	glVertex3f(40.0,640.0,-200.0);
	glEnd();
	//atas tutup kubah
	glBegin(GL_POLYGON);
	glColor3f (165.0/255.0, 164.0/255., 159.0/255.);
	glVertex3f(-50.0,740.0,-190.0);
	glVertex3f(-50.0,740.0,-260.0);
	glVertex3f(50.0,740.0,-260.0);
	glVertex3f(50.0,740.0,-190.0);
	glEnd();
	//jendela kiri
	glBegin(GL_POLYGON);
	glColor3f (0,0,0);
	glVertex3f(-30.0,730.0,-199.9);
	glVertex3f(-10.0,730.0,-199.9);
	glVertex3f(-10.0,660.0,-199.9);
	glVertex3f(-30.0,660.0,-199.9);
	glEnd();
	//jendela kanan
	glBegin(GL_POLYGON);
	glColor3f (0,0,0);
	glVertex3f(30.0,730.0,-199.9);
	glVertex3f(10.0,730.0,-199.9);
	glVertex3f(10.0,660.0,-199.9);
	glVertex3f(30.0,660.0,-199.9);
	glEnd();

}
void meja()
{
	glLineWidth(5);
	glColor3f(139.0 / 255.0, 69.0 / 255.0, 19.0 / 255.0);
	glBegin(GL_LINES);
	//vertical
	glVertex3f(30.0, -100.0, -180.0);
	glVertex3f(30.0, 0.0, -180.0);
	glVertex3f(30.0, -100.0, -150.0);
	glVertex3f(30.0, 0.0, -150.0);
	
	glVertex3f(80.0, -100.0, -180.0);
	glVertex3f(80.0, 0.0, -180.0);
	glVertex3f(80.0, -100.0, -150.0);
	glVertex3f(80.0, 0.0, -150.0);
	glEnd();

	glBegin(GL_POLYGON);
	glColor3f (1, 1, 10);
	glVertex3f(20.0,0.0,-190.0);
	glVertex3f(20.0,0.0,-140.0);
	glVertex3f(90.0,0.0,-140.0);
	glVertex3f(90.0,0.0,-190.0);
	glEnd();
}
void kursi()
{
	glLineWidth(5);
	glColor3f(139.0 / 255.0, 69.0 / 255.0, 19.0 / 255.0);
	glBegin(GL_LINES);
	//vertical
	glVertex3f(0.0, -100.0, -175.0);
	glVertex3f(0.0, -40.0, -175.0);
	glVertex3f(0.0, -100.0, -155.0);
	glVertex3f(0.0, -40.0, -155.0);
	
	glVertex3f(-35.0, -100.0, -175.0);
	glVertex3f(-35.0, 20.0, -175.0);
	glVertex3f(-35.0, -100.0, -155.0);
	glVertex3f(-35.0, 20.0, -155.0);
	glEnd();

	glBegin(GL_POLYGON);
	glColor3f (1, 1, 1);
	glVertex3f(5.0,-40.0,-153.0);
	glVertex3f(-35.0,-40.0,-153.0);
	glVertex3f(-35.0,-40.0,-178.0);
	glVertex3f(5.0,-40.0,-178.0);
	glEnd();

	glBegin(GL_POLYGON);
	glColor3f (1, 1, 1);
	glVertex3f(-32.8,20.0,-154.0);
	glVertex3f(-32.8,-20.0,-154.0);
	glVertex3f(-32.8,-20.0,-177.0);
	glVertex3f(-32.8,20.0,-177.0);
	glEnd();
}
void papantulis()
{
	//kanan
	glBegin(GL_POLYGON);
	glColor3f (1, 1, 1);
	glVertex3f(209.0,0.0,-150.0);
	glVertex3f(209.0,150.0,-150.0);
	glVertex3f(209.0,150.0,-250.0);
	glVertex3f(209.0,0.0,-250.0);
	glEnd();

	glLineWidth(3);
	glBegin(GL_LINE_LOOP);
	glColor3f (0, 0, 0);
	glVertex3f(209.0,0.0,-150.0);
	glVertex3f(209.0,150.0,-150.0);
	glVertex3f(209.0,150.0,-250.0);
	glVertex3f(209.0,0.0,-250.0);
	glEnd();
}
void lcd()
{
	glLineWidth(7);
	glColor3f(139.0 / 255.0, 69.0 / 255.0, 19.0 / 255.0);
	glBegin(GL_LINES);
	//vertical
	glVertex3f(0.0, 300.0, -200.0);
	glVertex3f(0.0, 150.0, -200.0);
	glEnd();

	glPointSize(20);
	glColor3f(0, 0, 0 );
	glBegin(GL_POINTS);	
	glVertex3f(0.0, 150.0, -199.0);
	glEnd();

}
void lemari()
{
	//lemariblkng
	glBegin(GL_POLYGON);
	glColor3f(139.0 / 255.0, 69.0 / 255.0, 19.0 / 255.0);
	glVertex3f(-160.0,-100.0,-299.0);
	glVertex3f(-160.0,120.0,-299.0);
	glVertex3f(-20.0,120.0,-299.0);
	glVertex3f(-20.0,-100.0,-299.0);
	glEnd();

	//lemaridepan
	glBegin(GL_POLYGON);
	glColor3f(139.0 / 255.0, 69.0 / 255.0, 19.0 / 255.0);
	glVertex3f(-160.0,-100.0,-240.0);
	glVertex3f(-160.0,120.0,-240.0);
	glVertex3f(-20.0,120.0,-240.0);
	glVertex3f(-20.0,-100.0,-240.0);
	glEnd();

	//lemarikiri
	glBegin(GL_POLYGON);
	glColor3f(139.0 / 255.0, 69.0 / 255.0, 19.0 / 255.0);
	glVertex3f(-160.0,-100.0,-299.0);
	glVertex3f(-160.0,120.0,-299.0);
	glVertex3f(-160.0,120.0,-240.0);
	glVertex3f(-160.0,-100.0,-240.0);
	glEnd();

	//lemaritengah
	glBegin(GL_POLYGON);
	glColor3f(139.0 / 255.0, 69.0 / 255.0, 19.0 / 255.0);
	glVertex3f(-20.0,-100.0,-299.0);
	glVertex3f(-20.0,120.0,-299.0);
	glVertex3f(-20.0,120.0,-240.0);
	glVertex3f(-20.0,-100.0,-240.0);
	glEnd();

	//lemariatas
	glBegin(GL_POLYGON);
	glColor3f(39.0 / 255.0, 69.0 / 255.0, 19.0 / 255.0);
	glVertex3f(-160.0,120.0,-299.0);
	glVertex3f(-160.0,120.0,-240.0);
	glVertex3f(-20.0,120.0,-240.0);
	glVertex3f(-20.0,120.0,-299.0);
	glEnd();

	//lemaribawah
	glBegin(GL_POLYGON);
	glColor3f(39.0 / 255.0, 69.0 / 255.0, 19.0 / 255.0);
	glVertex3f(-160.0,-100.0,-299.0);
	glVertex3f(-160.0,-100.0,-240.0);
	glVertex3f(-20.0,-100.0,-240.0);
	glVertex3f(-20.0,-100.0,-299.0);
	glEnd();

	glLineWidth(5);
	glColor3f(0,0,0);
	glBegin(GL_LINES);
	//vertical
	glVertex3f(-90.0, 120.0, -239.8);
	glVertex3f(-90.0, -100.0, -239.8);
	glEnd();

	glPointSize(5);
	glColor3f(0, 0, 0 );
	glBegin(GL_POINTS);	
	glVertex3f(-100.0, 10.0, -239.8);
	glVertex3f(-80.0, 10.0, -239.8);
	glEnd();
}
void tembokdalam()
{
	//kiri
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 195.0/255.0, 100.0/255.0);
	glVertex3f(-210.0,-100.0,-100.0);
	glVertex3f(-210.0,200.0,-100.0);
	glVertex3f(-210.0,200.0,-300.0);
	glVertex3f(-210.0,-100.0,-300.0);
	glEnd();

	//kanan
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 195.0/255.0, 100.0/255.0);
	glVertex3f(210.0,-100.0,-100.0);
	glVertex3f(210.0,200.0,-100.0);
	glVertex3f(210.0,200.0,-300.0);
	glVertex3f(210.0,-100.0,-300.0);
	glEnd();

	//atas
	glBegin(GL_POLYGON);
	glColor3f (1,1,1);
	glVertex3f(-210.0,200.0,-100.0);
	glVertex3f(210.0,200.0,-100.0);
	glVertex3f(210.0,200.0,-300.0);
	glVertex3f(-210.0,200.0,-300.0);
	glEnd();
}
void bola()
{
	glColor3f(1.0,1.0,1.0);
    glutSolidSphere(50.0,20,200);
}
void ling(int jari2, int jumlah_titik, int x_tengah, int y_tengah) {
 glBegin(GL_POLYGON);
 for (i=0;i<=360;i++){
 float sudut=i*(2*PI/jumlah_titik);
 float x=x_tengah+jari2*cos(sudut);
 float y=y_tengah+jari2*sin(sudut);
 glVertex2f(x,y);
 }
 glEnd();
 }
void lingkaran()
{
	glColor3f(1,1,1);
    ling(20, 200, 70, 118);
}

void keyboard(unsigned char key, int x, int y)
{
	switch (key)
	{
	case 'w':
	case 'W':
		zpos += 3.0;
		glTranslatef(0.0,0.0,3.0);
		break;
	case 'd':
	case 'D':
		xpos += 3.0;
		glTranslatef(3.0,0.0,0.0);
		break;
	case 's':
	case 'S':
		zpos += -3.0;
		glTranslatef(0.0,0.0,-3.0);
		break;
	case 'a':
	case 'A':
		xpos += -3.0;
		glTranslatef(-3.0,0.0,0.0);
		break;
	case '7':
		ypos += 3.0;
		glTranslatef(0.0,3.0,0.0);
		break;
	case '9':
		ypos -= 3.0;
		glTranslatef(0.0,-3.0,0.0);
		break;
	case '2':
		glRotatef(2.0,1.0,0.0,0.0);
		break;
	case '8':
		glRotatef(-2.0,1.0,0.0,0.0);
		break;
	case '6':
		glRotatef(2.0,0.0,1.0,0.0);
		break;
	case '4':
		glRotatef(-2.0,0.0,1.0,0.0);
		break;
	case '1':
		glRotatef(2.0,0.0,0.0,1.0);
		break;
	case '3':
		glRotatef(-2.0,0.0,0.0,1.0);
		break;
	case '5':
		if(is_depth)
		{
			is_depth = 0;
			glDisable(GL_DEPTH_TEST);
		}
		else
		{
			is_depth = 1;
			glEnable(GL_DEPTH_TEST);
		}
	}
	tampil();
}
void tampil(void)
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
	yak();
	glPushMatrix();
	atap();
	atas();
	tembokblkng();
	temboksmpgkiri();
	temboksmpgkanan();
	jendelatengah();
	temboktgh();
	jendelapolkiri();
	jendelapolkanan();
	jendelakiri();
	jendelakanan();
	meja();
	kursi();
	papantulis();
	lcd();
	lemari();
	tembokdalam();
	paralon();
	kubah();
	//bola();
	tabung();
	//lingkaran();

	glPopMatrix();

	glutSwapBuffers();
}
void idle()
{
    if (!mousedown)
    {
        xrot += 0.3f;
        yrot += 0.4f;
    }
    glutPostRedisplay();
}
void mouse(int button, int state, int x, int y) {
    if (button == GLUT_LEFT_BUTTON && state == GLUT_DOWN) {
        mousedown = true;
        xdiff = x - yrot;
        ydiff = -y + xrot;
    }
    else {
        mousedown = false;
    }
}
void mouseMotion(int x, int y) {
    if (mousedown) {
        yrot = x - xdiff;
        xrot = y + ydiff;

        glutPostRedisplay();
    }
}
void ukuran(int lebar, int tinggi){
    if(tinggi == 0) tinggi = 1;

    glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
    gluPerspective(160, lebar / tinggi, 5, 500);
    glTranslatef(0, -150, -150);
    glMatrixMode(GL_MODELVIEW);
}

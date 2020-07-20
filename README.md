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
    glEnable(GL_LIGHTING);
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
	glColor3f (134.0/255.0, 64.0/255., 22.0/255.);
	glVertex3f(-210.0,200.0,-80.0);
	glVertex3f(-410.0,500.0,-205.0);
	glVertex3f(-300.0,600.0,-225.0);
	glVertex3f(300.0,600.0,-225.0);
	glVertex3f(410.0,500.0,-205.0);
	glVertex3f(210.0,200.0,-80.0);
	glEnd();
	//atap blkng
	glBegin(GL_POLYGON);
	glColor3f (134.0/255.0, 64.0/255., 22.0/255.);
	glVertex3f(-410.0,200.0,-325.0);
	glVertex3f(-300.0,600.0,-225.0);
	glVertex3f(300.0,600.0,-225.0);
	glVertex3f(410.0,200.0,-325.0);
	glEnd();
	//atap depan tembok kiri
	glBegin(GL_POLYGON);
	glColor3f (134.0/255.0, 34.0/255.0, 22.0/255.0);
	glVertex3f(-210.0,200.0,-80.0);
	glVertex3f(-410.0,500.0,-205.0);
	glVertex3f(-1000.0,500.0,-30.0);
	glVertex3f(-750.0,200.0,10.0);
	glEnd();
	//atap belakang tembok kiri
	glBegin(GL_POLYGON);
	glColor3f (14.0/255.0, 34.0/255.0, 22.0/255.0);
	glVertex3f(-410.0,200.0,-300.0);
	glVertex3f(-410.0,500.0,-205.0);
	glVertex3f(-1000.0,500.0,-30.0);
	glVertex3f(-1200.0,200.0,-10.0);
	glEnd();

	glBegin(GL_TRIANGLES);
	glColor3f (22.0/255.0, 64.0/255., 22.0/255.);
	glVertex3f(-1200.0,200.0,-10.0);
	glVertex3f(-1000.0,500.0,-30.0);
	glVertex3f(-750.0,200.0,10.0);
	glEnd();

	//atap depan tembok kanan
	glBegin(GL_POLYGON);
	glColor3f (134.0/255.0, 34.0/255.0, 22.0/255.0);
	glVertex3f(210.0,200.0,-80.0);
	glVertex3f(410.0,500.0,-205.0);
	glVertex3f(1000.0,500.0,-30.0);
	glVertex3f(750.0,200.0,10.0);
	glEnd();
	//atap belakang tembok kanan
	glBegin(GL_POLYGON);
	glColor3f (14.0/255.0, 34.0/255.0, 22.0/255.0);
	glVertex3f(410.0,200.0,-300.0);
	glVertex3f(410.0,500.0,-205.0);
	glVertex3f(1000.0,500.0,-30.0);
	glVertex3f(1200.0,200.0,-10.0);
	glEnd();

	glBegin(GL_TRIANGLES);
	glColor3f (22.0/255.0, 64.0/255., 22.0/255.);
	glVertex3f(1200.0,200.0,-10.0);
	glVertex3f(1000.0,500.0,-30.0);
	glVertex3f(750.0,200.0,10.0);
	glEnd();

}
void atas()
{
	//atas
	glBegin(GL_QUADS);//ungu tengah kiri
	glColor3f (200.0/255.0, 0.0/255., 145.0/255.);
	glVertex3f(-210.0,210.0,-60.0);
	glVertex3f(-70.0,210.0,-60.0);
	glVertex3f(-70.0,200.0,-60.0);
	glVertex3f(-210.0,200.0,-60.0);
	glEnd();
	glBegin(GL_QUADS);//ungu tengah kanan
	glColor3f (200.0/255.0, 0.0/255., 145.0/255.);
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
	glColor3f (200.0/255.0, 0.0/255., 145.0/255.);
	glVertex3f(-590.0,210.0,-4.0);
	glVertex3f(-590.0,200.0,-4.0);
	glVertex3f(-750.0,200.0,20.0);
	glVertex3f(-750.0,210.0,20.0);
	glEnd();
	glBegin(GL_QUADS);//ungu kanan
	glColor3f (200.0/255.0, 0.0/255., 145.0/255.);
	glVertex3f(-210.0,210.0,-60.0);
	glVertex3f(-210.0,200.0,-60.0);
	glVertex3f(-430.0,200.0,-28.0);
	glVertex3f(-430.0,210.0,-28.0);
	glEnd();

	glBegin(GL_POLYGON);//putihpolkiri
	glColor3f (1.0,1.0,1.0);
	glVertex3f(-750.0,200.0,0.0);
	glVertex3f(-750.0,200.0,20.0);
	glVertex3f(-1200.0,200.0,0.0);
	glVertex3f(-1200.0,200.0,-10.0);
	glEnd();
	glBegin(GL_QUADS);//ungupolkiri
	glColor3f (200.0/255.0, 0.0/255., 15.0/255.);
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
	glColor3f (200.0/255.0, 0.0/255., 145.0/255.);
	glVertex3f(590.0,210.0,-4.0);
	glVertex3f(590.0,200.0,-4.0);
	glVertex3f(750.0,200.0,20.0);
	glVertex3f(750.0,210.0,20.0);
	glEnd();
	glBegin(GL_QUADS);//ungu kiri
	glColor3f (200.0/255.0, 0.0/255., 145.0/255.);
	glVertex3f(210.0,210.0,-60.0);
	glVertex3f(210.0,200.0,-60.0);
	glVertex3f(430.0,200.0,-28.0);
	glVertex3f(430.0,210.0,-28.0);
	glEnd();

	glBegin(GL_POLYGON);//putihpolkanan
	glColor3f (1.0,1.0,1.0);
	glVertex3f(750.0,200.0,0.0);
	glVertex3f(750.0,200.0,20.0);
	glVertex3f(1200.0,200.0,0.0);
	glVertex3f(1200.0,200.0,-10.0);
	glEnd();
	glBegin(GL_QUADS);//ungupolkanan
	glColor3f (200.0/255.0, 0.0/255., 15.0/255.);
	glVertex3f(750.0,210.0,20.0);
	glVertex3f(750.0,200.0,20.0);
	glVertex3f(1200.0,200.0,0.0);
	glVertex3f(1200.0,210.0,0.0);
	glEnd();


}
void temboktgh()
{
	//tengah kiri
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 195.0/255.0, 100.0/255.0);
	glVertex3f(-210.0,-100.0,-100.0);
	glVertex3f(-210.0,200.0,-100.0);
	glVertex3f(-70.0,200.0,-100.0);
	glVertex3f(-70.0,-100.0,-100.0);
	glEnd();

	//tengah
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 195.0/255.0, 10.0/255.0);
	glVertex3f(-70.0,-100.0,-60.0);
	glVertex3f(-70.0,250.0,-60.0);
	glVertex3f(70.0,250.0,-60.0);
	glVertex3f(70.0,-100.0,-60.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 195.0/255.0, 100.0/255.0);
	glVertex3f(-70.0,-100.0,-60.0);
	glVertex3f(-70.0,250.0,-60.0);
	glVertex3f(-70.0,250.0,-100.0);
	glVertex3f(-70.0,-100.0,-100.0);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 195.0/255.0, 100.0/255.0);
	glVertex3f(70.0,-100.0,-60.0);
	glVertex3f(70.0,250.0,-60.0);
	glVertex3f(70.0,250.0,-100.0);
	glVertex3f(70.0,-100.0,-100.0);
	glEnd();

	//tengah kanan
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 195.0/255.0, 100.0/255.0);
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
	glColor3f (200.0/255.0, 0.0/255.0, 0.0/255.0);
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
	glVertex3f(-550.0,250.0,-5.0);
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
	//full
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 0.0/255.0, 0.0/255.0);
	glVertex3f(210.0,-100.0,-100.0);
	glVertex3f(210.0,200.0,-100.0);
	glVertex3f(750.0,200.0,0.0);
	glVertex3f(750.0,-100.0,0.0);
	glEnd();

	//tengah
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 195.0/255.0, 100.0/255.0);
	glVertex3f(430.0,-100.0,-28.0);
	glVertex3f(430.0,250.0,-28.0);
	glVertex3f(470.0,250.0,-20.0);
	glVertex3f(515.0,400.0,-12.0);
	glVertex3f(550.0,250.0,-5.0);
	glVertex3f(590.0,250.0,0.0);
	glVertex3f(590.0,-100.0,0.0);
	glEnd();
	//kanan
	glBegin(GL_POLYGON);
	glColor3f (0.0/255.0, 5.0/255.0, 100.0/255.0);
	glVertex3f(430.0,-100.0,-28.0);
	glVertex3f(430.0,250.0,-28.0);
	glVertex3f(480.5,250.0,-55.0);
	glVertex3f(480.5,-100.0,-55.0);
	glEnd();
	//kiri
	glBegin(GL_POLYGON);
	glColor3f (0.0/255.0, 5.0/255.0, 100.0/255.0);
	glVertex3f(590.0,-100.0,0.0);
	glVertex3f(590.0,250.0,0.0);
	glVertex3f(650.0,250.0,-10.0);
	glVertex3f(650.0,-100.0,-10.0);
	glEnd();

	//tutup atas kiri
	glBegin(GL_POLYGON);
	glColor3f (90.0/255.0, 190.0/255.0, 10.0/255.0);
	glVertex3f(545.0,250.0,-3.0);
	glVertex3f(585.0,250.0,5.0);
	glVertex3f(660.0,250.0,-10.0);
	glVertex3f(600.0,250.0,-20.0);
	glEnd();
	//tutup segitiga atas kiri
	glBegin(GL_POLYGON);
	glColor3f (90.0/255.0, 10.0/255.0, 10.0/255.0);
	glVertex3f(545.0,250.0,-3.0);
	glVertex3f(600.0,250.0,-20.0);
	glVertex3f(540.0,400.0,-18.0);
	glVertex3f(510.0,400.0,-10.5);
	glEnd();

	//tutup atas kaanan
	glBegin(GL_POLYGON);
	glColor3f (90.0/255.0, 190.0/255.0, 10.0/255.0);
	glVertex3f(405.0,250.0,-27.0);
	glVertex3f(450.0,250.0,-19.0);
	glVertex3f(550.0,250.0,-30.0);
	glVertex3f(480.5,250.0,-70.0);
	glEnd();
	//tutup segitiga atas kanan
	glBegin(GL_POLYGON);
	glColor3f (90.0/255.0, 10.0/255.0, 10.0/255.0);
	glVertex3f(540.0,400.0,-18.0);
	glVertex3f(510.0,400.0,-10.5);
	glVertex3f(450.0,250.0,-19.0);
	glVertex3f(550.0,250.0,-30.0);

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

	//kanan
	glBegin(GL_POLYGON);
	glColor3f (200.0/255.0, 95.0/255.0, 10.0/255.0);
	glVertex3f(750.0,-100.0,0.0);
	glVertex3f(750.0,200.0,0.0);
	glVertex3f(1200.0,200.0,-10.0);
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
    glLineWidth(4);
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
	glVertex3f(-900.0,20.0,-2.0);
	glVertex3f(-900.0,85.0,-2.0);
	glVertex3f(-850.0,85.0,-2.0);//horizontal
	glVertex3f(-900.0,85.0,-2.0);
	glVertex3f(-850.0,20.0,-2.0);
	glVertex3f(-900.0,20.0,-2.0);

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
	glVertex3f(-1115.0,20.0,-6.0);
	glVertex3f(-1115.0,85.0,-6.0);
	glVertex3f(-1065.0,85.0,-5.5);//horizontal
	glVertex3f(-1115.0,85.0,-6.0);
	glVertex3f(-1115.0,20.0,-6.0);
	glVertex3f(-1065.0,20.0,-5.5);
	//bagianbawah
	glVertex3f(-850.0,-17.0,-2.0);//jendela 1 vertikal
	glVertex3f(-850.0,-82.0,-2.0);
	glVertex3f(-900.0,-82.0,-2.0);
	glVertex3f(-900.0,-17.0,-2.0);
	glVertex3f(-850.0,-82.0,-2.0);//horizontal
	glVertex3f(-900.0,-82.0,-2.0);
	glVertex3f(-850.0,-17.0,-2.0);
	glVertex3f(-900.0,-17.0,-2.0);

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
	glVertex3f(-1115.0,-82.0,-6.0);
	glVertex3f(-1115.0,-17.0,-6.0);
	glVertex3f(-1065.0,-82.0,-5.5);//horizontal
	glVertex3f(-1115.0,-82.0,-6.0);
	glVertex3f(-1115.0,-17.0,-6.0);
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
    glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-850.0,85.0,-2.0);//jendela 1 vertikal
	glVertex3f(-850.0,20.0,-2.0);
	glVertex3f(-900.0,20.0,-2.0);
	glVertex3f(-900.0,85.0,-2.0);
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
	glVertex3f(-1115.0,20.0,-6.1);
	glVertex3f(-1115.0,85.0,-6.1);
	glEnd();
	glBegin(GL_POLYGON);
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
	glVertex3f(-980.0,-82.0,-5.0);
	glVertex3f(-980.0,-17.0,-5.0);
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
	glVertex3f(-1115.0,-17.0,-6.1);
	glVertex3f(-1115.0,-82.0,-6.1);
	glEnd();

	glLineWidth(2);
	glColor3f(1.0,1.0,1.0);
	glBegin(GL_LINES);
	glVertex3f(-805.0,175.0,0.1);
	glVertex3f(-805.0,110.0,0.1);
	glVertex3f(-780.0,142.0,0.1);
	glVertex3f(-830.0,142.0,0.1);
	glVertex3f(-975.0,175.0,-3.9);
	glVertex3f(-975.0,110.0,-3.9);
	glVertex3f(-950.0,142.0,-3.9);
	glVertex3f(-1000.0,142.0,-3.9);
	glVertex3f(-1143.0,175.0,-7.5);
	glVertex3f(-1143.0,110.0,-7.5);
    glVertex3f(-1170.0,142.0,-9.0);
	glVertex3f(-1120.0,142.0,-8.0);
	glVertex3f(-870.0,85.0,-1.0);
	glVertex3f(-870.0,20.0,-1.0);
	glVertex3f(-850.0,55.0,-1.0);
	glVertex3f(-895.0,55.0,-1.0);
	glVertex3f(-955.0,85.0,-4.5);
	glVertex3f(-955.0,20.0,-4.5);
	glVertex3f(-930.0,55.0,-4.0);
	glVertex3f(-985.0,55.0,-4.5);
	glVertex3f(-1003.0,85.0,-4.0);
	glVertex3f(-1003.0,20.0,-4.0);
	glVertex3f(-980.0,55.0,-4.0);
	glVertex3f(-1030.0,55.0,-4.0);
	glVertex3f(-1090.0,85.0,-5.5);
	glVertex3f(-1090.0,20.0,-5.5);
	glVertex3f(-1065.0,55.0,-5.5);
	glVertex3f(-1115.0,55.0,-6.0);
	glVertex3f(-870.0,-82.0,-1.0);
	glVertex3f(-870.0,-15.0,-1.0);
	glVertex3f(-850.0,-49.0,-1.0);
	glVertex3f(-893.0,-49.0,-1.0);
	glVertex3f(-955.0,-82.0,-4.5);
	glVertex3f(-955.0,-17.0,-4.5);
	glVertex3f(-930.0,-49.0,-4.0);
	glVertex3f(-985.0,-49.0,-4.5);
	glVertex3f(-1003.0,-82.0,-4.0);
	glVertex3f(-1003.0,-17.0,-4.0);
	glVertex3f(-985.0,-49.0,-4.2);
	glVertex3f(-1030.0,-49.0,-4.0);
	glVertex3f(-1090.0,-82.0,-5.5);
	glVertex3f(-1090.0,-17.0,-5.5);
	glVertex3f(-1065.0,-49.0,-5.5);
	glVertex3f(-1115.0,-49.0,-6.0);
	glEnd();
}
void jendelapolkanan()
{
    glLineWidth(4);
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
	glVertex3f(900.0,20.0,-2.0);
	glVertex3f(900.0,85.0,-2.0);
	glVertex3f(850.0,85.0,-2.0);//horizontal
	glVertex3f(900.0,85.0,-2.0);
	glVertex3f(850.0,20.0,-2.0);
	glVertex3f(900.0,20.0,-2.0);

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
	glVertex3f(1115.0,20.0,-6.0);
	glVertex3f(1115.0,85.0,-6.0);
	glVertex3f(1065.0,85.0,-5.5);//horizontal
	glVertex3f(1115.0,85.0,-6.0);
	glVertex3f(1115.0,20.0,-6.0);
	glVertex3f(1065.0,20.0,-5.5);

	//bagianbawah
	glVertex3f(850.0,-17.0,-2.0);//jendela 1 vertikal
	glVertex3f(850.0,-82.0,-2.0);
	glVertex3f(900.0,-82.0,-2.0);
	glVertex3f(900.0,-17.0,-2.0);
	glVertex3f(850.0,-82.0,-2.0);//horizontal
	glVertex3f(900.0,-82.0,-2.0);
	glVertex3f(850.0,-17.0,-2.0);
	glVertex3f(900.0,-17.0,-2.0);

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
	glVertex3f(1115.0,-82.0,-6.0);
	glVertex3f(1115.0,-17.0,-6.0);
	glVertex3f(1065.0,-82.0,-5.5);//horizontal
	glVertex3f(1115.0,-82.0,-6.0);
	glVertex3f(1115.0,-17.0,-6.0);
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
    glBegin(GL_POLYGON);
	glColor3f(0.0,0.0,0.0);
	glVertex3f(850.0,85.0,-2.0);//jendela 1 vertikal
	glVertex3f(850.0,20.0,-2.0);
	glVertex3f(900.0,20.0,-2.0);
	glVertex3f(900.0,85.0,-2.0);
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
	glVertex3f(1115.0,20.0,-6.1);
	glVertex3f(1115.0,85.0,-6.1);
	glEnd();
	glBegin(GL_POLYGON);
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
	glVertex3f(980.0,-82.0,-5.0);
	glVertex3f(980.0,-17.0,-5.0);
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
	glVertex3f(1115.0,-17.0,-6.1);
	glVertex3f(1115.0,-82.0,-6.1);
	glEnd();
	glLineWidth(2);
	glColor3f(1.0,1.0,1.0);
	glBegin(GL_LINES);
	glVertex3f(805.0,175.0,0.1);
	glVertex3f(805.0,110.0,0.1);
	glVertex3f(780.0,142.0,0.1);
	glVertex3f(830.0,142.0,0.1);
	glVertex3f(975.0,175.0,-3.9);
	glVertex3f(975.0,110.0,-3.9);
	glVertex3f(950.0,142.0,-3.9);
	glVertex3f(1000.0,142.0,-3.9);
	glVertex3f(1143.0,175.0,-7.5);
	glVertex3f(1143.0,110.0,-7.5);
    glVertex3f(1170.0,142.0,-9.0);
	glVertex3f(1120.0,142.0,-8.0);
	glVertex3f(870.0,85.0,-1.0);
	glVertex3f(870.0,20.0,-1.0);
	glVertex3f(850.0,55.0,-1.0);
	glVertex3f(895.0,55.0,-1.0);
	glVertex3f(955.0,85.0,-4.5);
	glVertex3f(955.0,20.0,-4.5);
	glVertex3f(930.0,55.0,-4.0);
	glVertex3f(985.0,55.0,-4.5);
	glVertex3f(1003.0,85.0,-4.0);
	glVertex3f(1003.0,20.0,-4.0);
	glVertex3f(980.0,55.0,-4.0);
	glVertex3f(1030.0,55.0,-4.0);
	glVertex3f(1090.0,85.0,-5.5);
	glVertex3f(1090.0,20.0,-5.5);
	glVertex3f(1065.0,55.0,-5.5);
	glVertex3f(1115.0,55.0,-6.0);
	glVertex3f(870.0,-82.0,-1.0);
	glVertex3f(870.0,-15.0,-1.0);
	glVertex3f(850.0,-49.0,-1.0);
	glVertex3f(893.0,-49.0,-1.0);
	glVertex3f(955.0,-82.0,-4.5);
	glVertex3f(955.0,-17.0,-4.5);
	glVertex3f(930.0,-49.0,-4.0);
	glVertex3f(985.0,-49.0,-4.5);
	glVertex3f(1003.0,-82.0,-4.0);
	glVertex3f(1003.0,-17.0,-4.0);
	glVertex3f(985.0,-49.0,-4.2);
	glVertex3f(1030.0,-49.0,-4.0);
	glVertex3f(1090.0,-82.0,-5.5);
	glVertex3f(1090.0,-17.0,-5.5);
	glVertex3f(1065.0,-49.0,-5.5);
	glVertex3f(1115.0,-49.0,-6.0);
	glEnd();
}
void jendelatengah()
{
	glLineWidth(5);
	glColor3f(139.0/255.0,69.0/255.0,19.0/255.0);
	glBegin(GL_LINES);
	//vertical
	glVertex3f(-177.0,-75.0,-99.8);
	glVertex3f(-177.0,175.0,-99.8);
	glVertex3f(-75.0,175.0,-99.8);
	glVertex3f(-75.0,-75.0,-99.8);
	glVertex3f(-142.0,-75.0,-99.8);
	glVertex3f(-142.0,175.0,-99.8);
	glVertex3f(-108.0,175.0,-99.8);
	glVertex3f(-108.0,-75.0,-99.8);
	//horizontal
	glVertex3f(-177.0,175.0,-99.8);
	glVertex3f(-75.0,175.0,-99.8);
	glVertex3f(-177.0,110.0,-99.8);
	glVertex3f(-75.0,110.0,-99.8);
	glVertex3f(-177.0,18.0,-99.8);
	glVertex3f(-75.0,18.0,-99.8);
	glVertex3f(-177.0,-75.0,-99.8);
	glVertex3f(-75.0,-75.0,-99.8);
	glEnd();

	glLineWidth(2);
	glColor3f(139.0/255.0,69.0/255.0,19.0/255.0);
	glBegin(GL_LINES);
	glVertex3f(-177.0,-40.0,-99.8);
	glVertex3f(-75.0,-40.0,-99.8);
	glEnd();

	glBegin(GL_POLYGON);
	glColor3f (1, 1, 1);
	glVertex3f(-177.0,175.0,-99.8);
	glVertex3f(-75.0,175.0,-99.8);
	glVertex3f(-75.0,-75.0,-99.8);
	glVertex3f(-177.0,-75.0,-99.8);
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
	glLineWidth(5);
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
	glLineWidth(5);
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
	glLineWidth(5);
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
	glLineWidth(5);
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
	glLineWidth(5);
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
	//jendela 2 bawah -------------------------------------------------------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-695,-17.0,-10.0);
	glVertex3f(-695,-82.0,-10.0);
	glVertex3f(-670,-82.0,-14.0);
	glVertex3f(-670,-17.0,-14.0);
    glEnd();
	glLineWidth(5);
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
	glBegin(GL_POLYGON);//jendela 1 atas--------------------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-580.0,175.0,-1.5);
	glVertex3f(-580.0,90.0,-1.5);
	glVertex3f(-545.0,90.0,-7.3);
	glVertex3f(-545.0,175.0,-7.3);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-580.0,175.0,-1.5);
	glVertex3f(-580.0,90.0,-1.5);
	glVertex3f(-545.0,90.0,-7.3);
	glVertex3f(-545.0,175.0,-7.3);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-560.0,175.0,-4.8);
    glVertex3f(-560.0,90.0,-4.8);
    glVertex3f(-545.0,90.0,-7.3);
    glVertex3f(-545.0,135.0,-7.3);
    glVertex3f(-580.0,135.0,-1.5);
    glVertex3f(-580.0,175.0,-1.5);
	glEnd();
    glBegin(GL_POLYGON);//jendela 2 atas------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-530.0,175.0,-9.0);
	glVertex3f(-530.0,90.0,-9.0);
	glVertex3f(-490.0,90.0,-15.5);
	glVertex3f(-490.0,175.0,-15.5);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-530.0,175.0,-9.0);
	glVertex3f(-530.0,90.0,-9.0);
	glVertex3f(-490.0,90.0,-15.5);
	glVertex3f(-490.0,175.0,-15.5);
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-510.0,175.0,-12.2);
    glVertex3f(-510.0,90.0,-12.2);
    glVertex3f(-490.0,90.0,-15.5);
    glVertex3f(-490.0,135.0,-15.5);
    glVertex3f(-530.0,135.0,-9.0);
    glVertex3f(-530.0,175.0,-9.0);
	glEnd();
	glBegin(GL_POLYGON);//jendela 3 atas------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-475.0,175.0,-19.0);
	glVertex3f(-475.0,90.0,-19.0);
	glVertex3f(-435.0,90.0,-26.5);
	glVertex3f(-435.0,175.0,-26.5);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-475.0,175.0,-19.0);
	glVertex3f(-475.0,90.0,-19.0);
	glVertex3f(-435.0,90.0,-26.5);
	glVertex3f(-435.0,175.0,-26.5);
	glEnd();
    glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-453.0,175.0,-22.9);
    glVertex3f(-453,90.0,-22.9);
    glVertex3f(-435.0,90.0,-26.5);
    glVertex3f(-435.0,135.0,-26.5);
    glVertex3f(-475.0,135.0,-19.0);
    glVertex3f(-475.0,175.0,-19.0);
	glEnd();

	glBegin(GL_POLYGON);//jendela 1 tengah--------------------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-580.0,70.0,-1.5);
	glVertex3f(-580.0,-15.0,-1.5);
	glVertex3f(-545.0,-15.0,-7.3);
	glVertex3f(-545.0,70.0,-7.3);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-580.0,70.0,-1.5);
	glVertex3f(-580.0,-15.0,-1.5);
	glVertex3f(-545.0,-15.0,-7.3);
	glVertex3f(-545.0,70.0,-7.3);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-560.0,70.0,-4.8);
    glVertex3f(-560.0,-15.0,-4.8);
    glVertex3f(-545.0,-15.0,-7.3);
    glVertex3f(-545.0,27.0,-7.3);
    glVertex3f(-580.0,27.0,-1.5);
    glVertex3f(-580.0,70.0,-1.5);
	glEnd();
	 glBegin(GL_POLYGON);//jendela 2 tengah------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-530.0,70.0,-9.1);
	glVertex3f(-530.0,-15.0,-9.1);
	glVertex3f(-490.0,-15.0,-15.5);
	glVertex3f(-490.0,70.0,-15.5);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-530.0,70.0,-9.1);
	glVertex3f(-530.0,-15.0,-9.1);
	glVertex3f(-490.0,-15.0,-15.5);
	glVertex3f(-490.0,70.0,-15.5);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-510.0,70.0,-12.2);
    glVertex3f(-510.0,-15.0,-12.2);
    glVertex3f(-490.0,-15.0,-15.5);
    glVertex3f(-490.0,27.0,-15.5);
    glVertex3f(-530.0,27.0,-9.0);
    glVertex3f(-530.0,70.0,-9.0);
	glEnd();
	glBegin(GL_POLYGON);//jendela 3 tengah------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(-475.0,70.0,-19.0);
	glVertex3f(-475.0,-15.0,-19.0);
	glVertex3f(-435.0,-15.0,-26.5);
	glVertex3f(-435.0,70.0,-26.5);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-475.0,70.0,-19.0);
	glVertex3f(-475.0,-15.0,-19.0);
	glVertex3f(-435.0,-15.0,-26.5);
	glVertex3f(-435.0,70.0,-26.5);
	glEnd();
    glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(-453.0,70.0,-22.9);
    glVertex3f(-453.0,-15.0,-22.9);
    glVertex3f(-435.0,-15.0,-26.5);
    glVertex3f(-435.0,27.0,-26.5);
    glVertex3f(-475.0,27.0,-19.0);
    glVertex3f(-475.0,70.0,-19.0);
	glEnd();

	//jendela belakang
	glBegin(GL_POLYGON);//atas1 --------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(-470.0,175.0,-51.5);
	glVertex3f(-470.0,110.0,-51.5);
	glVertex3f(-440.0,110.0,-57.2);
	glVertex3f(-440.0,175.0,-57.2);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-420.0,175.0,-60.0);
	glVertex3f(-420.0,110.0,-60.0);
	glVertex3f(-365.0,110.0,-69.8);
	glVertex3f(-365.0,175.0,-69.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-345.0,175.0,-75.0);
	glVertex3f(-345.0,110.0,-75.0);
	glVertex3f(-290.0,110.0,-83.8);
	glVertex3f(-290.0,175.0,-83.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-270.0,175.0,-86.5);
	glVertex3f(-270.0,110.0,-86.5);
	glVertex3f(-220.0,110.0,-95.6);
	glVertex3f(-220.0,175.0,-95.6);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-420.0,80.0,-60.0);
	glVertex3f(-420.0,20.0,-60.0);
	glVertex3f(-365.0,20.0,-69.8);
	glVertex3f(-365.0,80.0,-69.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-345.0,80.0,-75.0);
	glVertex3f(-345.0,20.0,-75.0);
	glVertex3f(-290.0,20.0,-83.8);
	glVertex3f(-290.0,80.0,-83.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-270.0,80.0,-86.5);
	glVertex3f(-270.0,20.0,-86.5);
	glVertex3f(-220.0,20.0,-95.6);
	glVertex3f(-220.0,80.0,-95.6);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-420.0,-17.0,-60.0);
	glVertex3f(-420.0,-82.0,-60.0);
	glVertex3f(-365.0,-82.0,-69.8);
	glVertex3f(-365.0,-17.0,-69.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-345.0,-17.0,-75.0);
	glVertex3f(-345.0,-82.0,-75.0);
	glVertex3f(-290.0,-82.0,-83.8);
	glVertex3f(-290.0,-17.0,-83.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(-270.0,-82.0,-86.5);
	glVertex3f(-270.0,-17.0,-86.5);
	glVertex3f(-220.0,-17.0,-95.6);
	glVertex3f(-220.0,-82.0,-95.6);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
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
	glLineWidth(5);
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
	glBegin(GL_POLYGON);//jendela 3 atas------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(475.0,175.0,-19.0);
	glVertex3f(475.0,90.0,-19.0);
	glVertex3f(435.0,90.0,-26.5);
	glVertex3f(435.0,175.0,-26.5);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(475.0,175.0,-19.0);
	glVertex3f(475.0,90.0,-19.0);
	glVertex3f(435.0,90.0,-26.5);
	glVertex3f(435.0,175.0,-26.5);
	glEnd();
    glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(453.0,175.0,-22.9);
    glVertex3f(453,90.0,-22.9);
    glVertex3f(435.0,90.0,-26.5);
    glVertex3f(435.0,135.0,-26.5);
    glVertex3f(475.0,135.0,-19.0);
    glVertex3f(475.0,175.0,-19.0);
	glEnd();

	 //jendela 1 tengah -------------------------------------------------------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(735,85.0,-2.5);
	glVertex3f(735,20.0,-2.5);
	glVertex3f(710,20.0,-7.0);
	glVertex3f(710,85.0,-7.0);
    glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
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
	glLineWidth(5);
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
	//jendela 2 bawah -------------------------------------------------------
    glBegin(GL_POLYGON);
    glColor3f(0.0,0.0,0.0);
    glVertex3f(695,-17.0,-10.0);
	glVertex3f(695,-82.0,-10.0);
	glVertex3f(670,-82.0,-14.0);
	glVertex3f(670,-17.0,-14.0);
    glEnd();
	glLineWidth(5);
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
	glBegin(GL_POLYGON);//jendela 1 atas--------------------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(580.0,175.0,-1.5);
	glVertex3f(580.0,90.0,-1.5);
	glVertex3f(545.0,90.0,-7.3);
	glVertex3f(545.0,175.0,-7.3);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(580.0,175.0,-1.5);
	glVertex3f(580.0,90.0,-1.5);
	glVertex3f(545.0,90.0,-7.3);
	glVertex3f(545.0,175.0,-7.3);
	glVertex3f(580.0,175.0,-1.5);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(560.0,175.0,-4.8);
    glVertex3f(560.0,90.0,-4.8);
    glVertex3f(545.0,90.0,-7.3);
    glVertex3f(545.0,135.0,-7.3);
    glVertex3f(580.0,135.0,-1.5);
    glVertex3f(580.0,175.0,-1.5);
	glEnd();
    glBegin(GL_POLYGON);//jendela 2 atas------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(530.0,175.0,-9.0);
	glVertex3f(530.0,90.0,-9.0);
	glVertex3f(490.0,90.0,-15.5);
	glVertex3f(490.0,175.0,-15.5);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(530.0,175.0,-9.0);
	glVertex3f(530.0,90.0,-9.0);
	glVertex3f(490.0,90.0,-15.5);
	glVertex3f(490.0,175.0,-15.5);
	glVertex3f(530.0,175.0,-9.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(510.0,175.0,-12.2);
    glVertex3f(510.0,90.0,-12.2);
    glVertex3f(490.0,90.0,-15.5);
    glVertex3f(490.0,135.0,-15.5);
    glVertex3f(530.0,135.0,-9.0);
    glVertex3f(530.0,175.0,-9.0);
	glEnd();


	glBegin(GL_POLYGON);//jendela 1 tengah--------------------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(580.0,70.0,-1.5);
	glVertex3f(580.0,-15.0,-1.5);
	glVertex3f(545.0,-15.0,-7.3);
	glVertex3f(545.0,70.0,-7.3);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(580.0,70.0,-1.5);
	glVertex3f(580.0,-15.0,-1.5);
	glVertex3f(545.0,-15.0,-7.3);
	glVertex3f(545.0,70.0,-7.3);
	glVertex3f(580.0,70.0,-1.5);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(560.0,70.0,-4.8);
    glVertex3f(560.0,-15.0,-4.8);
    glVertex3f(545.0,-15.0,-7.3);
    glVertex3f(545.0,27.0,-7.3);
    glVertex3f(580.0,27.0,-1.5);
    glVertex3f(580.0,70.0,-1.5);
	glEnd();
	 glBegin(GL_POLYGON);//jendela 2 tengah------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(530.0,70.0,-9.1);
	glVertex3f(530.0,-15.0,-9.1);
	glVertex3f(490.0,-15.0,-15.5);
	glVertex3f(490.0,70.0,-15.5);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(530.0,70.0,-9.1);
	glVertex3f(530.0,-15.0,-9.1);
	glVertex3f(490.0,-15.0,-15.5);
	glVertex3f(490.0,70.0,-15.5);
	glVertex3f(530.0,70.0,-9.0);
	glEnd();
	glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(510.0,70.0,-12.2);
    glVertex3f(510.0,-15.0,-12.2);
    glVertex3f(490.0,-15.0,-15.5);
    glVertex3f(490.0,27.0,-15.5);
    glVertex3f(530.0,27.0,-9.0);
    glVertex3f(530.0,70.0,-9.0);
	glEnd();
	glBegin(GL_POLYGON);//jendela 3 tengah------------------------------------
    glColor3f(0.0,0.0,0.0);
    glVertex3f(475.0,70.0,-19.0);
	glVertex3f(475.0,-15.0,-19.0);
	glVertex3f(435.0,-15.0,-26.5);
	glVertex3f(435.0,70.0,-26.5);
	glEnd();
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(475.0,70.0,-19.0);
	glVertex3f(475.0,-15.0,-19.0);
	glVertex3f(435.0,-15.0,-26.5);
	glVertex3f(435.0,70.0,-26.5);
	glEnd();
    glLineWidth(2);
	glBegin(GL_LINE_LOOP);
	glVertex3f(453.0,70.0,-22.9);
    glVertex3f(453.0,-15.0,-22.9);
    glVertex3f(435.0,-15.0,-26.5);
    glVertex3f(435.0,27.0,-26.5);
    glVertex3f(475.0,27.0,-19.0);
    glVertex3f(475.0,70.0,-19.0);
	glEnd();

	//jendela belakang
	glBegin(GL_POLYGON);//atas1 --------------------------
	glColor3f(0.0,0.0,0.0);
	glVertex3f(470.0,175.0,-51.5);
	glVertex3f(470.0,110.0,-51.5);
	glVertex3f(440.0,110.0,-57.2);
	glVertex3f(440.0,175.0,-57.2);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(420.0,175.0,-60.0);
	glVertex3f(420.0,110.0,-60.0);
	glVertex3f(365.0,110.0,-69.8);
	glVertex3f(365.0,175.0,-69.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(345.0,175.0,-75.0);
	glVertex3f(345.0,110.0,-75.0);
	glVertex3f(290.0,110.0,-83.8);
	glVertex3f(290.0,175.0,-83.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(270.0,175.0,-86.5);
	glVertex3f(270.0,110.0,-86.5);
	glVertex3f(220.0,110.0,-95.6);
	glVertex3f(220.0,175.0,-95.6);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(420.0,80.0,-60.0);
	glVertex3f(420.0,20.0,-60.0);
	glVertex3f(365.0,20.0,-69.8);
	glVertex3f(365.0,80.0,-69.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(345.0,80.0,-75.0);
	glVertex3f(345.0,20.0,-75.0);
	glVertex3f(290.0,20.0,-83.8);
	glVertex3f(290.0,80.0,-83.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(270.0,80.0,-86.5);
	glVertex3f(270.0,20.0,-86.5);
	glVertex3f(220.0,20.0,-95.6);
	glVertex3f(220.0,80.0,-95.6);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(420.0,-17.0,-60.0);
	glVertex3f(420.0,-82.0,-60.0);
	glVertex3f(365.0,-82.0,-69.8);
	glVertex3f(365.0,-17.0,-69.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(345.0,-17.0,-75.0);
	glVertex3f(345.0,-82.0,-75.0);
	glVertex3f(290.0,-82.0,-83.8);
	glVertex3f(290.0,-17.0,-83.8);
	glEnd();
	glLineWidth(5);
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
	glLineWidth(5);
	glBegin(GL_LINE_LOOP);
	glColor3f(1.0,1.0,1.0);
	glVertex3f(270.0,-82.0,-86.5);
	glVertex3f(270.0,-17.0,-86.5);
	glVertex3f(220.0,-17.0,-95.6);
	glVertex3f(220.0,-82.0,-95.6);
	glEnd();
	glLineWidth(5);
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
	glVertex3f(0.0, 150.0, -195.0);
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
	temboktgh();
	tembokblkng();
	temboksmpgkiri();
	temboksmpgkanan();
	jendelatengah();
	jendelapolkiri();
	jendelapolkanan();
	jendelakiri();
	jendelakanan();
	meja();
	kursi();
	papantulis();
	lcd();
	lemari();

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

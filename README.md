#include <windows.h>
#ifdef __APPLE__
#include <GLUT/glut.h>
#else
#include <GL/glut.h>
#endif
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
	glVertex3f(-460.0,250.0,-20.0);
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
	glVertex3f(460.0,250.0,-20.0);
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
    gluPerspective(130, lebar / tinggi, 5, 500);
    glTranslatef(0, -150, -150);
    glMatrixMode(GL_MODELVIEW);
}

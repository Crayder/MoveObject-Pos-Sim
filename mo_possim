/*
 * Copyright (C) 2015 - Crayder
 * 
 * This program is free software; you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation; either version 2 of the License, or
 * (at your option) any later version.
 * 
 * This program is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 * 
 * You should have received a copy of the GNU General Public License along
 * with this program; if not, write to the Free Software Foundation, Inc.,
 * 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
 */

enum MovementInfo
{
	Float:CeX_aX,	//Start position
	Float:CeX_aY,	//Start position
	Float:CeX_aZ,	//Start position
	Float:CeX_bX,	//End position
	Float:CeX_bY,	//End position
	Float:CeX_bZ,	//End position
	
	Float:CeX_arX,	//Start rotation
	Float:CeX_arY,	//Start rotation
	Float:CeX_arZ,	//Start rotation
	Float:CeX_brX,	//End rotation
	Float:CeX_brY,	//End rotation
	Float:CeX_brZ,	//End rotation
	
	Float:CeX_S,	//Speed
	CeX_sT			//Start time
}
static CeX_O[MAX_OBJECTS][MovementInfo];

static stock CeX_MoveObject(objectid, Float:X, Float:Y, Float:Z, Float:Speed, Float:RotX = -1000.0, Float:RotY = -1000.0, Float:RotZ = -1000.0)
{
	static Float:cX, Float:cY, Float:cZ;
	
	GetObjectPos(objectid, cX, cY, cZ);
	CeX_O[objectid][CeX_aX] = cX;
	CeX_O[objectid][CeX_aY] = cY;
	CeX_O[objectid][CeX_aZ] = cZ;
	CeX_O[objectid][CeX_bX] = X;
	CeX_O[objectid][CeX_bY] = Y;
	CeX_O[objectid][CeX_bZ] = Z;
	
	GetObjectRot(objectid, cX, cY, cZ);
	CeX_O[objectid][CeX_arX] = cX;
	CeX_O[objectid][CeX_arY] = cY;
	CeX_O[objectid][CeX_arZ] = cZ;
	CeX_O[objectid][CeX_brX] = RotX;
	CeX_O[objectid][CeX_brY] = RotY;
	CeX_O[objectid][CeX_brZ] = RotZ;
	
	CeX_O[objectid][CeX_S] = Speed;
	CeX_O[objectid][CeX_sT] = GetTickCount();
	
	return MoveObject(objectid, X, Y, Z, Speed, RotX, RotY, RotZ);
}

#if defined _ALS_MoveObject
	#undef MoveObject
#else
	#define _ALS_MoveObject
#endif
#define MoveObject CeX_MoveObject

static stock CeX_GetObjectPos(objectid, &Float:X, &Float:Y, &Float:Z)
{
	if(IsObjectMoving(objectid))
	{
		static Float:uV[3],
			elapse = GetTickCount() - CeX_O[objectid][CeX_sT],
			Float:D = floatsqroot(
				floatpower(CeX_O[objectid][CeX_bX] - CeX_O[objectid][CeX_aX], 2.0) + 
				floatpower(CeX_O[objectid][CeX_bY] - CeX_O[objectid][CeX_aY], 2.0) + 
				floatpower(CeX_O[objectid][CeX_bZ] - CeX_O[objectid][CeX_aZ], 2.0)) * 1000
		;
	
		uV[0] = ((CeX_O[objectid][CeX_bX] - CeX_O[objectid][CeX_aX]) / D) * elapse * CeX_O[objectid][CeX_S];
		uV[1] = ((CeX_O[objectid][CeX_bY] - CeX_O[objectid][CeX_aY]) / D) * elapse * CeX_O[objectid][CeX_S];
		uV[2] = ((CeX_O[objectid][CeX_bZ] - CeX_O[objectid][CeX_aZ]) / D) * elapse * CeX_O[objectid][CeX_S];
	
		X = CeX_O[objectid][CeX_aX] + uV[0];
		Y = CeX_O[objectid][CeX_aY] + uV[1];
		Z = CeX_O[objectid][CeX_aZ] + uV[2];

		return 1;
	}
	return GetObjectPos(objectid, X, Y, Z);
}

#if defined _ALS_GetObjectPos
	#undef GetObjectPos
#else
	#define _ALS_GetObjectPos
#endif
#define GetObjectPos CeX_GetObjectPos

static stock CeX_GetObjectRot(objectid, &Float:X, &Float:Y, &Float:Z)
{
	if(IsObjectMoving(objectid))
	{
		static Float:uV[3],
			elapse = GetTickCount() - CeX_O[objectid][CeX_sT],
			Float:D = floatsqroot(
				floatpower(CeX_O[objectid][CeX_bX] - CeX_O[objectid][CeX_aX], 2.0) + 
				floatpower(CeX_O[objectid][CeX_bY] - CeX_O[objectid][CeX_aY], 2.0) + 
				floatpower(CeX_O[objectid][CeX_bZ] - CeX_O[objectid][CeX_aZ], 2.0)) * 1000
		;
	
		uV[0] = ((CeX_O[objectid][CeX_brX] - CeX_O[objectid][CeX_arX]) / D) * elapse * CeX_O[objectid][CeX_S];
		uV[1] = ((CeX_O[objectid][CeX_brY] - CeX_O[objectid][CeX_arY]) / D) * elapse * CeX_O[objectid][CeX_S];
		uV[2] = ((CeX_O[objectid][CeX_brZ] - CeX_O[objectid][CeX_arZ]) / D) * elapse * CeX_O[objectid][CeX_S];
	
		X = CeX_O[objectid][CeX_arX] + uV[0];
		Y = CeX_O[objectid][CeX_arY] + uV[1];
		Z = CeX_O[objectid][CeX_arZ] + uV[2];

		return 1;
	}
	return GetObjectRot(objectid, X, Y, Z);
}

#if defined _ALS_GetObjectRot
	#undef GetObjectRot
#else
	#define _ALS_GetObjectRot
#endif
#define GetObjectRot CeX_GetObjectRot

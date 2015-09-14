# MoveObject-Pos-Sim
Simulates GetObjectPos for MoveObject during movement. The position will not be exactly to the point, but it's an extremely accurate estimate (I think subtracting a millisecond from the tickcount would actually help but I haven't tested it).

# Intructions
All you need to do is include this and the functions (`MoveObject`, `GetObjectPos`, and `GetObjectRot`) will be hooked and ready to use.

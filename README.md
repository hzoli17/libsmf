# libsmf - Standard MIDI file library

## What's this?

libsmf is a library for read and write standard MIDI files on C++.

## Example

### Simple dump example

```C++
#include "SMF.h"
#include <iostream>
#include <fstream>
using namespace std;
int main(int argc, char * argv[])
{
	cout<<"libsmf demo 1.0"<<endl<<endl;
	SMF::MIDI midi;
	unsigned err;
	if (argc<2)
	{
		cout<<"Usage: "<<argv[0]<<" file"<<endl;
		return 1;
	}
	if ((err=SMF::loadFile(argv[1], &midi))!=SMF_OK)
	{
		cerr<<SMF::errStr(err)<<endl;
		return 1;
	}
	cout<<"File format: "<<dec<<(int)midi.format<<endl;
	cout<<"Song tempo (TPQ): "<<dec<<midi.tempo<<endl<<endl;
	for (unsigned int i=0;i<midi.tracks.size();i++)
	{
		cout<<"Track "<<i+1<<endl<<endl;
		for (unsigned int j=0;j<midi.tracks[i].size();j++)
		{
			cout<<hex<<"0x"<<j<<": "<<dec<<midi.tracks[i][j].deltaTime<<' ';
			for (unsigned int k=0;k<midi.tracks[i][j].data.size();k++)
			{
				cout<<hex<<"0x"<<(int)(unsigned char)midi.tracks[i][j].data[k]<<' ';
			}
			cout<<endl;
		}
		cout<<endl;
	}
	return 0;
}
```
### Usage:
`./midi_dump test.mid`
